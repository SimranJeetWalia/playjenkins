pipeline {
	agent {
		kubernetes {
		yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  jenkins: app
spec:
  serviceAccountName: jenkins-admin
  containers:
  - name: jenkins-app
    image: docker:dind
"""
}
}
stages {
	stage('Build Container Builder') {
		steps {
			container('jenkins-slave') {
				script{
					sampleapp = docker.build("simranjeetwalia/sample-app:${env.$BUILD_ID}")
					}
					}
					}
					}
					}
					}
