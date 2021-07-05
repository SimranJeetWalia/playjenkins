pipeline {
	agent {
		kubernetes {
		label 'jenkins-slave'
		defaultContainer 'jnlp'
		yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  jenkins: slave
spec:
  serviceAccountName: jenkins-admin
  containers:
  - name: jenkins-slave
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


