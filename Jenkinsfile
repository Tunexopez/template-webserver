pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key') // Ensure 'server-key' exists in Jenkins credentials
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh '''
                # Print current directory and list files
                pwd
                ls
                
                # Create a ZIP file of the project
                zip -r webapp.zip .
                
                # List files to verify the ZIP creation
                ls
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sshagent(['SSH_CRED']) {
                    sh '''
                    # Transfer the ZIP file to the remote server
                    scp webapp.zip user@remote-server:/path/to/deployment/

                    # Log in to the server, unzip the file, and clean up
                    ssh user@remote-server "unzip -o /path/to/deployment/webapp.zip -d /path/to/deployment/ && rm /path/to/deployment/webapp.zip"
                    '''
                }
            }
        }

        stage('Clean-Up') {
            steps {
                echo 'Cleaning up workspace...'
                deleteDir() // Deletes all files in the Jenkins workspace
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
