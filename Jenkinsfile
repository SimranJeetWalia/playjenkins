pipeline {
  agent {
    kubernetes {
    label 'jenkinsnode'
    yaml """
apiVersion: v1
kind: Pod
metadata:
  name: jenkinsnode
  labels:
    name: jenkinsnode
spec:
  serviceAccountName: default
  containers:
  - name: kubectl
    image: simranjeetwalia/kubectl:v1
    securityContext:
      privileged: true
"""
}
}
stages {
  stage('Deploy to k8s') {
    steps {
      container('kubectl') {
        script {
          kubeconfig(credentialsId: 'kubeconfigsecret', serverUrl: 'https://172.31.23.124:6443') {
            sh 'kubectl create -f radhey.yml'
}
        }
      }
    }
  }
  }
  }
