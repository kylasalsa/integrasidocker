pipeline {
  agent any
  environment {
    IMAGE_NAME = 'kylasalsa/keladockercc'
    REGISTRY = 'https://index.docker.io/v1/'
    REGISTRY_CREDENTIALS = 'dockerhub-credentials'
  }
  stages {
    stage('Checkout') {
      steps {
        echo 'Mengambil kode dari repository...'
      }
    }
    stage('Build Docker Image') {
      steps {
        script {
          docker.build("${IMAGE_NAME}:${env.BUILD_NUMBER}")
        }
      }
    }
    stage('Push Docker Image') {
    steps {
        script {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                bat 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                bat 'docker push kylasalsa/keladockercc:${BUILD_NUMBER}'
                bat 'docker push kylasalsa/keladockercc:latest'
            }
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
