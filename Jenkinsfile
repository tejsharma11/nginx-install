pipeline {
  agent any

  environment {
    IMAGE = "mynginx"
    KUBECONFIG = "C:\\Windows\\System32\\config\\systemprofile\\.kube\\config"
  }

  stages {
    stage('Build Docker Image') {
      steps {
        bat "docker build -t ${IMAGE}:latest ."
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
