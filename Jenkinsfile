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
                bat 'docker build -t victoryhon/jenkins-demo .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    bat 'docker login -u victoryhon -p Singapore88$'
                    bat 'docker push victoryhon/jenkins-demo'
                }
            }
        }
    }
}
