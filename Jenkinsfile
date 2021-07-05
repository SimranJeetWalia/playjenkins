	pipeline {

		agent {
	    kubernetes {
	      //label 'sample-app'
	      defaultContainer 'jnlp'
	      yaml """
	apiVersion: v1
	kind: Pod
	metadata:
	labels:
	  name: sample-app
	spec:
	  serviceAccountName: jenkins-admin
	  containers:
	  - name: sample-app
	    image: docker:dind
	"""
	}
	  }
	  stages {

	  stage('Build Container Builder') {
	      steps {
	        container('sample-app') {
	        	script{
	        		sampleapp = docker.build("simranjeetwalia/sample-app:${env.$BUILD_ID}")
	        }
	      }
	    }
	}
}
}
