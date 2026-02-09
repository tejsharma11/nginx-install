pipeline {
  agent any

  environment {
    IMAGE = "mynginx"
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/tejsharma11/nginx-install.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        bat "docker build -t $IMAGE:latest ."
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        bat '''
          kubectl apply -f k8s/deployment.yaml
          kubectl apply -f k8s/service.yaml
        '''
      }
    }
  }
}
