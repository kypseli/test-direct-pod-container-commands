pipeline {
  agent {
    kubernetes {
      label 'test-running-pod-command'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  serviceAccountName: cjoc
  containers:
  - name: kubectl
    image: gcr.io/cloud-builders/kubectl
    command:
    - cat
    tty: true
  securityContext:
   runAsUser: 1000
"""
}
  }
  stages {
    stage('Clean') {
      steps {
        container('kubectl') {
          sh('kubectl -n cje get psp')
          sh('kubectl -n cje apply -f kubectl.yml')
        } 
      }
    }
  }
}
