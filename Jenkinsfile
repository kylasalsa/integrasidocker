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
          docker.withRegistry(REGISTRY, REGISTRY_CREDENTIALS) {
            def tag = "${IMAGE_NAME}:${env.BUILD_NUMBER}"
            docker.image(tag).push()
            docker.image(tag).push('latest')
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
