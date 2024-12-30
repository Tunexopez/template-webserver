pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Test Credentials') {
            steps {
                sshagent(['server-key']) {
                    sh 'ssh -T git@github.com'
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building app'
                sh 'pwd'
                sh 'ls'
                sh 'zip -r webapp.zip .'
                sh 'ls'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying app'
                // Deployment commands
            }
        }

        stage('Clean-Up') {
            steps {
                echo 'Removing existing files'
                deleteDir()
            }
        }
    }
}
