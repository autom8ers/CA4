pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('autom8ers-dockerhub')        
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh "docker build -t autom8ers/autom8ers:${env.BUILD_NUMBER} ."
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'autom8ers-dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh "docker login -u $USERNAME -p $PASSWORD"
                        sh "docker push autom8ers/autom8ers:${env.BUILD_NUMBER}"
                    }
                }
            }
        }
    }
}
