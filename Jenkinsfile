pipeline {
	agent {
		kubernetes {
		defaultContainer 'jnlp'
		yaml """
apiVersion: v1
kind: Pod
spec:
  serviceAccountName: default
  containers:
  - name: "jenkins-agent"
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
