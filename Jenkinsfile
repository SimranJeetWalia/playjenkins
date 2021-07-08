pipeline {
	agent {
		kubernetes {
		label 'jenkinsnode'
		yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: jenkinsnode
spec:
  serviceAccountName: jenkins-admin
  containers:
  - name: jenkinsnode
    image: docker:dind
    securityContext:
      privileged: true
"""
}
}
stages {
	stage('Build Container Builder') {
		steps {
			container('jenkinsnode') {
				script{
					sampleapp = docker.build("simranjeetwalia/sample-app:${env.$BUILD_ID}")
					}
					}
					}
					}
					}
					}
