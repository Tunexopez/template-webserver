pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
        def CONNECT = 'ssh -o StrictHostKeyChecking=no ubuntu@3.96.186.155'
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
                sshagent(['server-key']) {
                        sh 'scp -o StrictHostKeyChecking=no -i $SSH_CRED webapp.zip ubuntu@3.96.186.155/:/home/ubuntu'
                        sh '''
                        $CONNECT <<EOF
                        sudo apt update && sudo apt install zip -y
                        sudo rm -rf /var/www/html/
                        sudo mkdir -p /var/www/html/
                        sudo unzip webapp.zip -d /var/www/html/
                        EOF
                    '''

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
