pipeline {
    agent any
    
    environment {
        DOCKER_HUB_USERNAME = credentials('autom8ers')
        DOCKER_HUB_PASSWORD = credentials('Salis2002$')
        DOCKER_HUB_REPO = 'autom8ers/mongodb'
        DOCKER_IMAGE_TAG = 'latest'
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG}", "./path/to/your/Dockerfile")
                }
            }
        }
        
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_USERNAME, DOCKER_HUB_PASSWORD) {
                        docker.image("${DOCKER_HUB_REPO}:${DOCKER_IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}
