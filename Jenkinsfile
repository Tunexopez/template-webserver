pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
    }stages {
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
                // Add deployment commands here
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