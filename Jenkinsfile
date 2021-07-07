pipeline {
	agent {
		kubernetes {
		label 'vinay'
		yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: radhey
spec:
  serviceAccountName: kubernetes-admin
  containers:
  - name: radhey
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
//	stage('Push image') {
//            steps {
//                script {
//                	container('radhey') {
//                		docker.withRegistry('https://registry.hub.docker.com', 'dockerhubcred') {
//                			sampleapp.push("${env.BUILD_ID}")
//                    }
//                }
//            }
//        }
//        }
  stage('Deploy App') {
	  steps {
		  script {
			  container('radhey') {
				  kubernetesDeploy(configs: "radhey.yml")
	      
      }
    }
    }
  }
}
}
