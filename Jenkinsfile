pipeline {
  agent any

  stages {
    stage('Deploy to Kubernetes') {
      steps {
        withCredentials([file(credentialsId: 'kubeconfig-file', variable: 'KUBECONFIG')]) {
          sh '''
            kubectl version --short
            kubectl cluster-info
            kubectl apply -f k8s/service.yaml
          '''
        }
      }
    }
  }
}
