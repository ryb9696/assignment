pipeline {
    agent any

    parameters {
        choice(name: 'BRANCH', choices: ['dev', 'qa', 'uat', 'prod'], description: 'Select branch to build')
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the selected branch
                    checkout([$class: 'GitSCM', branches: [[name: params.BRANCH]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/ryb9696/assignment.git']]])
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh "chmod +x deploy.sh" // Ensure execute permission for the script
                    sh "./deploy.sh" // Execute the deploy script

                    echo "Build successful"
                }
            }
        }

        stage('Test') {
            when {
                expression { params.BRANCH ==~ /^(qa|uat|prod)$/ }
            }
            steps {
                script {
                    sh "chmod +x deploy.sh" // Ensure execute permission for the script
                    sh "./deploy.sh" // Execute the deploy script

                    echo "Test successful"
                }
            }
        }

        stage('Deploy') {
            when {
                expression { params.BRANCH ==~ /^(uat|prod)$/ }
            }
            steps {
                script {
                    sh "chmod +x deploy.sh" // Ensure execute permission for the script
                    sh "./deploy.sh" // Execute the deploy script

                    echo "Deploy successful"
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace after the build
            cleanWs()
        }
    }
}

