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
                sshagent(['server-key']) {
                    sh 'scp -o StrictHostKeyChecking=no -i $SSH_CRED webapp.zip ubuntu@3.96.186.155:/home/ubuntu/'
                    sh 'ssh -o StrictHostKeyChecking=no -i $SSH_CRED ubuntu@3.96.186.155 "sudo apt install zip -y"'
                    sh 'ssh -o StrictHostKeyChecking=no -i $SSH_CRED ubuntu@3.96.186.155 "sudo rm -rf /var/www/html/"'
                    sh 'ssh -o StrictHostKeyChecking=no -i $SSH_CRED ubuntu@3.96.186.155 "sudo mkdir /var/www/html/"'
                    sh 'ssh -o StrictHostKeyChecking=no -i $SSH_CRED ubuntu@3.96.186.155 "sudo unzip /home/ubuntu/webapp.zip -d /var/www/html/"'
                }
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
