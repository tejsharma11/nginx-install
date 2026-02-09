pipeline {
  agent any

  environment {
    IMAGE = "mynginx"
  }

  stages {
    stage('Build Docker Image') {
      steps {
        bat "docker build -t $IMAGE:latest ."
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        bat '''
          kubectl apply -f k8s/deployment.yaml --validate=false
          kubectl apply -f k8s/service.yaml --validate=false
        '''
      }
    }
  }
}
