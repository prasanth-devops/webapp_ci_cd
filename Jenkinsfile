pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/prasanth‑devops/webapp_ci_cd.git'
            }
        }

        stage('Deploy to EC2') {
            steps {
                // Replace with your actual deploy commands
                sh 'scp -o StrictHostKeyChecking=no -i /path/to/your/key.pem index.html style.css app.js ubuntu@100.26.182.226:/var/www/html/'
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
