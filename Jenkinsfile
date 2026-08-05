pipeline {
    agent none

    environment{
        DEPLOY_ENV = "staging"
    }
    stages{
        stage('Backend'){
            agent{
                docker{
                    image 'python:3.11-slim'
                    reuseNode true
                }
            }
            steps{
                echo 'building and testing backend..'
                sh 'python --version'
                dir('backend'){
                    sh 'python test.py'
                }
            }
        }
        stage('Frontend'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                echo 'building and testing frontend..'
                sh 'node -v'
                dir('frontend'){
                    sh 'npm run test'
                }
            }
        }
        stage('Deployment'){
            agent any
            steps{
                echo "Deploying application to ${DEPLOY_ENV} environment..."
                echo "Pipeline complete"
            }
        }
    }
    post {
        always {
            echo 'pipeline teardown complete'
        }
    }
}