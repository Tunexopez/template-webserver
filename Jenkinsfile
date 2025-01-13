pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key') // Ensure the correct credential ID is provided
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building app...'
                sh '''
                pwd
                ls
                zip -r webapp.zip .
                ls
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying app...'
                // Add deployment commands here
            }
        }

        stage('Clean-Up') {
            steps {
                echo 'Cleaning up workspace...'
                deleteDir()
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Build and deployment were successful!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
