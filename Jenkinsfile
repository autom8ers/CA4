pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('autom8ers-dockerhub')        
    }
    stages {
        stage('Pulling MongoDB Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        docker.image('mongo:latest').pull()
                    }
                }
            }
        }
        stage('Building MongoDB Image') {
            steps {
                script {
                    docker.build('autom8ers/mongo:latest', '.')
                }
            }
        }
        stage('Pushing MongoDB Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        docker.image('autom8ers/mongo:latest').push()
                    }
                }
            }
        }
    }
}

