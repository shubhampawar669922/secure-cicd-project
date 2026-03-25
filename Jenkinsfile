pipeline {
    agent any

    environment {
        IMAGE = "shubham1244/secure-cicd-project"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/shubhampawar669922/secure-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE:latest .'
            }
        }

        stage('Scan Image (Trivy)') {
            steps {
                sh 'trivy image --severity HIGH,CRITICAL $IMAGE:latest'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker login -u shubham1244 -p dckr_pat_IkPxeVFJ8nN6mPm3g4ZGC4dSp08'
                sh 'docker push $IMAGE:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}
