pipeline {
    agent any
    environment {
        APP_NAME = "my-app"
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm install'  // Example for Node.js projects
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sshagent(['your-ssh-credential-id']) {
                    sh '''
                    scp -r build/ user@server:/var/www/my-app
                    ssh user@server "sudo systemctl restart my-app"
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
