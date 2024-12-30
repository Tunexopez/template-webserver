pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
    }
    stages {
        stage('Prepare Environment') {
            steps {
                echo 'Installing dependencies'
                sh 'sudo apt update && sudo apt install zip -y'
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
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
