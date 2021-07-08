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
  serviceAccountName: jenkins-admin
  containers:
  - name: dockerdind
    image: docker:dind
    securityContext:
      privileged: true
  - name: kubectl
    image: simranjeetwalia/kubectl:v1
"""
}
}
stages {
  stage('Build Docker Image') {
    steps {
      container('dockerdind') {
        script {
          sampleapp = docker.build("simranjeetwalia/sample-app:${env.$BUILD_ID}")
        }
      }
    }
  }
  stage('Push Docker Image to registery') {
    steps {
      container('dockerdind') {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhubcred') {
                      sampleapp.push("${env.BUILD_ID}")
                    }
        }
      }
    }
  }
  stage('Deploy to k8s') {
    steps {
      container('kubectl') {
        script {
          kubeconfig(credentialsId: 'kubeconfigsecret', serverUrl: 'https://172.31.23.124:6443') {
            sh 'kubectl create -f myweb.yaml'
            }
        }
      }
    }
  }
  }
  }
