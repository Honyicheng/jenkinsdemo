FROM nginx:alpine
COPY . /usr/share/nginx/html

Update your Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Verify') {
            steps {
                bat 'dir'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t dewixaltius/jenkins-demo .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    bat 'docker login -u victoryhon -p Singapore88$'
                    bat 'docker push dewixaltius/jenkins-demo'
                }
            }
        }
    }
}
