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
                    checkout([$class: 'GitSCM', branches: [[name: params.BRANCH]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'your_repo_url']]])
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
                    // Run test-specific actions here
                    echo "Testing..."
                }
            }
        }

        stage('Deploy') {
            when {
                expression { params.BRANCH ==~ /^(uat|prod)$/ }
            }
            steps {
                script {
                    // Run deployment-specific actions here
                    echo "Deploying..."
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

            }
        }
    }
}

