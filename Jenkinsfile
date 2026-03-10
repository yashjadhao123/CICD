pipeline {
    agent any

    environment {
        APP_DIR = "/var/www/html"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning application code from GitHub..."
                git branch: 'main',
                    url: 'https://github.com/yashjadhao123/CICD.git'
            }
        }

        stage('Install Apache') {
            steps {
                sh 'sudo yum install -y httpd || true'
            }
        }

        stage('Start Apache Service') {
            steps {
                sh '''
                sudo systemctl start httpd
                sudo systemctl enable httpd
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                sudo rm -rf ${APP_DIR}/*
                sudo cp -r * ${APP_DIR}/
                sudo chown -R apache:apache ${APP_DIR}
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'sudo systemctl status httpd'
            }
        }
    }
}
