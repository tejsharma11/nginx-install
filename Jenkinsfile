pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t nginx-jenkins .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker rm -f nginx-container || exit 0
                docker run -d -p 8080:80 --name nginx-container nginx-jenkins
                '''
            }
        }
    }
}
