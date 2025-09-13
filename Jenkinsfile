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
                bat 'docker build -t victoryhon/html-demo:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    bat 'docker login -u %DOCKER_USERNAME% -p %DOCKER_PASSWORD%'
                    bat 'docker push victoryhon/html-demo:latest'
                }
            }
        }

         stage('Deploy Docker Image') {
            steps {
                  bat 'docker rm -f app 2>NUL'
                  bat 'docker run -d --name app -p 8888:80 html-demo:latest'
        
                }
            }
        }
    }
