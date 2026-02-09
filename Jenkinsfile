pipeline {
  agent any

    stage('Build Docker Image') {
      steps {
        bat 'docker build -t mynginx:latest .'
      }
    }

    stage('Run Container') {
      steps {
        bat 'docker stop mynginx || exit 0'
        bat 'docker rm mynginx || exit 0'
        bat 'docker run -d --name mynginx -p 8080:80 mynginx:latest'
      }
    }
  }
}
