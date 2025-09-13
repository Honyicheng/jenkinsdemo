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
                    bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                    bat 'docker push victoryhon/jenkins-demo'
                }
            }
        }

         stage('Deploy Docker Image') {
            steps {
                  bat 'docker build -f Dockerfile -t html-app:latest .'
                  bat 'docker rm -f app'
                  bat 'docker run -d -p "8888:80 --name app html-app:lastest'
        
                }
            }
        }
    }
}
