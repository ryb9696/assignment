pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def branchName = env.GIT_BRANCH
                    def environment = null

                    switch (branchName) {
                        case 'dev':
                            environment = 'dev'
                            break
                        case 'qa':
                            environment = 'qa'
                            break
                        case 'uat':
                            environment = 'uat'
                            break
                        case 'prod':
                            environment = 'prod'
                            break
                    }

                    if (environment) {
                        sh """
                            #!/bin/bash

                            echo "Deploying to $environment environment..."

                            # TODO: Implement the deployment logic here.

                            echo "Deployed to $environment environment successfully!"
                        """
                    }
                }
            }
        }

        stage('Clean up') {
            steps {
                echo 'Cleaning up...'
            }
        }
    }
}

