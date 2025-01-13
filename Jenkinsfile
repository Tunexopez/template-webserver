pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key') // Replace 'server-key' with your Jenkins credential ID
        REMOTE_SERVER = 'user@remote-server' // Replace with the remote server's username and address
        DEPLOY_DIR = '/path/to/deployment'  // Replace with the deployment directory on the remote server
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh '''
                # Display the current directory
                pwd

                # List the files in the workspace
                ls -lah

                # Create a zip archive of the project
                zip -r webapp.zip .

                # Confirm the zip file is created
                ls -lh webapp.zip
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application to the remote server...'
                sshagent([SSH_CRED]) {
                    sh '''
                    # Transfer the zip file to the remote server
                    scp webapp.zip ${REMOTE_SERVER}:${DEPLOY_DIR}/

                    # SSH into the remote server, extract the zip, and clean up
                    ssh ${REMOTE_SERVER} "
                    mkdir -p ${DEPLOY_DIR} &&
                    unzip -o ${DEPLOY_DIR}/webapp.zip -d ${DEPLOY_DIR} &&
                    rm -f ${DEPLOY_DIR}/webapp.zip &&
                    echo 'Deployment completed successfully.'
                    "
                    '''
                }
            }
        }

        stage('Clean-Up') {
            steps {
                echo 'Cleaning up the workspace...'
                deleteDir() // Cleans the Jenkins workspace
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
