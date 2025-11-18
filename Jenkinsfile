pipeline {
    agent any

    environment {
        // Jenkins SSH credentials ID
        SSH_CREDENTIALS_ID = 'ec2-ssh-key'  
        EC2_USER = 'ubuntu'
        EC2_HOST = '100.26.182.226'
        DEPLOY_PATH = '/var/www/html/'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout your GitHub repo
                git branch: 'master', url: 'https://github.com/prasanth-devops/webapp_ci_cd.git', credentialsId: ''
            }
        }

        stage('Deploy to EC2') {
            steps {
                // Use SSH credentials to deploy code
                sshagent([env.SSH_CREDENTIALS_ID]) {
                    sh """
                        # Copy all project files to EC2 web directory
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
