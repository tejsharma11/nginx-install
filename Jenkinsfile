stage('Build Image') {
  steps {
    sh 'docker build -t tejsharma22/nginx:latest .'
  }
}

stage('Push Image') {
  steps {
    sh 'docker push tejsharma22/nginx:latest'
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
