pipeline {
  agent any
  environment {
    IMAGE_NAME = 'kylasalsa/keladockercc'
  }
  stages {
    stage('Checkout') {
      steps {
        echo 'Mengambil kode dari repository...'
      }
    }
    stage('Build Docker Image') {
      steps {
        bat 'docker build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
      }
    }
    stage('Push Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
          bat 'docker push %IMAGE_NAME%:%BUILD_NUMBER%'
          bat 'docker tag %IMAGE_NAME%:%BUILD_NUMBER% %IMAGE_NAME%:latest'
          bat 'docker push %IMAGE_NAME%:latest'
        }
      }
    }
  }
  post {
    always {
      echo 'Pipeline selesai dijalankan 🚀'
    }
  }
}
