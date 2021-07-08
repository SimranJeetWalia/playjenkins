pipeline {
  agent {
    kubernetes {
    label 'jenkinsnode'
    yaml """
apiVersion: v1
kind: Pod
metadata:
  name: jenkinsnode
spec:
  serviceAccountName: jenkins-admin
  containers:
  - name: dockerdind
    image: docker:dind
    securityContext:
      privileged: true
"""
}
}
stages {
  stage('Build Container Builder') {
    steps {
      container('radhey') {
        script{
          sampleapp = docker.build("simranjeetwalia/sample-app:${env.BUILD_ID}")
          }
          }
          }
          }
  stage('Deploy to k8s') {
    steps {
      container('kubectl') {
        script {
          sh 'kubectl create -f ppp.yml'
        }
      }
    }
  }
  }
  }
