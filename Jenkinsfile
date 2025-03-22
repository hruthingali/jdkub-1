pipeline {
    agent any
    environment {
        IMAGE_NAME = "flask-app20"
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
               git branch: 'main', url: 'https://github.com/hruthingali/jdkub-1.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-app20:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                sh 'docker tag flask-app:latest hruthingali/flask-app20:latest'
                sh 'docker push hruthingali/flask-app20:latest'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
