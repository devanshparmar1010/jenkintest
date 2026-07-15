pipeline {
    agent any

    tools {
        nodejs 'Node22'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Backend - Install & Build') {
            steps {
                dir('backend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Frontend - Install & Build') {
            steps {
                dir('frontend') {
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Analytics - Install & Validate') {
            steps {
                dir('analytics') {
                    bat 'pip install -r requirements.txt'
                    bat 'python validate_deps.py'
                }
            }
        }
    }

    post {
        success {
            echo 'CIPipeline passed successfully.'
        }
        failure {
            echo 'CI Pipelinefailed. Check logs above.'
        }
    }
}
