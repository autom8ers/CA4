pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_CREDENTIALS = credentials('autom8ers-dockerhub')
    }
    
    stages {
        stage('Docker Login') {
            steps {
                sh 'echo $DOCKER_REGISTRY_CREDENTIALS | docker login --username autom8ers --password-stdin'
            }
        }
        
        stage('Build and Push Frontend Docker Image') {
            steps {
                dir('Frontend') {
                    script {
                        // Build the frontend Docker image
                        sh 'docker build -t autom8ers/frontend-image:latest .'
                        // Push the frontend Docker image to Docker Hub
                        sh 'docker push autom8ers/frontend-image:latest'
                    }
                }
            }
        }
        
        stage('Build and Push Backend Docker Image') {
            steps {
                dir('Backend') {
                    script {
                        // Build the backend Docker image
                        sh 'docker build -t autom8ers/backend-image:latest .'
                        // Push the backend Docker image to Docker Hub
                        sh 'docker push autom8ers/backend-image:latest'
                    }
                }
            }
        }
        
        stage('Docker Logout') {
            steps {
                sh 'docker logout'
            }
        }
    }
}