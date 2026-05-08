pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'cd app && mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t sufiii/devsecops-app .'
            }
        }

        stage('Trivy Scan') {
            steps {
                bat 'trivy image sufiii/devsecops-app'
            }
        }

        stage('Docker Push') {
            steps {
                bat 'docker push sufiii/devsecops-app'
            }
        }

        stage('Deploy') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }
}