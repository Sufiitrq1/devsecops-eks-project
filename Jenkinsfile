pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'cd app && mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t sufiii/devsecops-app .'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh 'trivy image sufiii/devsecops-app'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push sufiii/devsecops-app'
            }
        }

        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}