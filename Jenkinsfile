pipeline {
    agent any
    environment {
        SSH_CRED = credentials('server-key')
    } def CONNECT = 'ssh -o StrictHostKeyChecking=no ubuntu@15.223.185.145'
    stages {
        
        stage('Build') {
            steps {
                echo 'building app'
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
                    sh 'scp -o StrictHostKeyChecking=no -i $SSH_CRED webapp.zip ubuntu@15.223.185.145:/home/ubuntu'
                    sh '''
                    $CONNECT << EOF
                    sudo apt install zip -y
                    sudo rm -rf /var/www/html/
                    sudo mkdir /var/www/html/
                    sudo unzip webapp.zip -d /var/www/html/
                    EOF
                    '''
                }
            }
        }

