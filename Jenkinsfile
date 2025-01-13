pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building app'
                sh "pwd"
                sh "ls"
                sh "zip -r webapp.zip ."
                sh "ls"
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying app'
                sh """
                scp -i ${SSH_CRED} webapp.zip user@remote-server:/path/to/deploy/
                ssh -i ${SSH_CRED} user@remote-server "unzip -o /path/to/deploy/webapp.zip -d /path/to/deploy/"
                """
            }
        }

        stage('Clean-Up') {
            steps {
                echo 'Removing existing files'
                deleteDir()
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished. Check the logs for details.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
