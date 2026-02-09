pipeline {
  agent any

  environment {
    KUBE_API = "https://kubernetes.docker.internal:6443"
    NAMESPACE = "default"
  }

  stages {
    stage('Deploy') {
      steps {
        withCredentials([string(credentialsId: 'k8s-token', variable: 'TOKEN')]) {
          sh '''
            cat <<EOF > /tmp/kubeconfig
            apiVersion: v1
            kind: Config
            clusters:
            - name: docker-desktop
              cluster:
                server: ${KUBE_API}
                insecure-skip-tls-verify: true
            contexts:
            - name: ci
              context:
                cluster: docker-desktop
                user: ci-user
                namespace: ${NAMESPACE}
            current-context: ci
            users:
            - name: ci-user
              user:
                token: ${TOKEN}
            EOF

            export KUBECONFIG=/tmp/kubeconfig
            kubectl version --short
            kubectl apply -f k8s/service.yaml
          '''
        }
      }
    }
  }
}
