pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'hruthingali/flask-app20:latest'
    }
    stages {
        stage('Clone Repository') {
            steps {
               git branch: 'main', url: 'https://github.com/hruthingali/jdkub-1.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push $DOCKER_IMAGE'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
