stage('Build Image') {
  steps {
    sh 'docker build -t dockerhubuser/nginx:latest .'
  }
}

stage('Push Image') {
  steps {
    sh 'docker push dockerhubuser/nginx:latest'
  }
}

stage('Deploy to Kubernetes') {
  steps {
    sh '''
      kubectl apply -f k8s/deployment.yaml
      kubectl apply -f k8s/service.yaml
    '''
  }
}
