pipeline {
    agent any

    environment {
        EC2_USER = 'ubuntu'
        EC2_HOST = '100.26.182.226'   // Replace with your EC2 public IP
        DEPLOY_PATH = '/var/www/html/webapp'  // Or wherever you want to deploy
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/prasanth-devops/webapp_ci_cd.git'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-ssh-key']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} 'mkdir -p ${DEPLOY_PATH}'
                        scp -o StrictHostKeyChecking=no -r * ${EC2_USER}@${EC2_HOST}:${DEPLOY_PATH}
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment succeeded!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
