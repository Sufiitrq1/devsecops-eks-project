pipeline {
    agent any

    tools {
        maven 'M3'
    }

    environment {
        APP_NAME = "sufiii/devsecops-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build (Maven)') {
            steps {
                bat 'cd app && mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                bat "docker build -t %APP_NAME% ."
            }
        }

        stage('Trivy Scan') {
            steps {
                bat "trivy image %APP_NAME%"
            }
        }

        stage('Docker Push') {
            steps {
                bat "docker push %APP_NAME%"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline SUCCESS 🚀'
        }
        failure {
            echo 'Pipeline FAILED ❌ - check logs'
        }
    }
}