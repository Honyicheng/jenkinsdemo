pipeline {
  agent any

  environment {
    IMAGE     = 'victoryhon/html-demo'
    TAG       = 'latest'
    APP_NAME  = 'app'
    HOST_PORT = '8888'   // change if busy
    CONTAINER_PORT = '80'
  }

  stages {
    stage('Verify') {
      steps { bat 'dir' }
    }

    stage('Build Docker Image') {
      steps {
        bat 'docker build -t %IMAGE%:%TAG% .'
      }
    }

    stage('Push Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials',
                  usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
          bat """
            echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin
            docker push %IMAGE%:%TAG%
          """
        }
      }
    }

    stage('Deploy Docker Image') {
      steps {
        bat """
          docker rm -f %APP_NAME% 2>NUL || ver >NUL
          docker run -d --name %APP_NAME% -p %HOST_PORT%:%CONTAINER_PORT% %IMAGE%:%TAG%
        """
        // Optional: quick smoke check (needs PowerShell on agent)
        bat 'powershell -Command "iwr http://localhost:%HOST_PORT% -UseBasicParsing | Out-Null"'
      }
    }
  }
}
