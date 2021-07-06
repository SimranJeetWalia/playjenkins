pipeline {
	agent {
		kubernetes {
		yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: radhey
spec:
  serviceAccountName: jenkins-admin
  containers:
  - name: radhey
    image: docker:dind
"""
}
}
stages {
	stage('Build Container Builder') {
		steps {
			container('radhey') {
				script{
					sampleapp = docker.build("simranjeetwalia/sample-app:${env.$BUILD_ID}")
					}
					}
					}
					}
					}
					}
