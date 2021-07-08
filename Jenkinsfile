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
  - name: dockerdind
    image: docker:dind
    securityContext:
      privileged: true
  - name: kubectl
    image: roffe/kubectl
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
	//stage('Push image') {
        //    steps {
        //        script {
        //        	container('radhey') {
        //        		docker.withRegistry('https://registry.hub.docker.com', 'dockerhubcred') {
        //       			sampleapp.push("${env.BUILD_ID}")
        //            }
        //        }
        //    }
       // }
       // }
  stage ('Deploy to k8s cluster')
    steps {
      container('kubectl')
        #sh "sed -i 's/#latest/${BUILD_NUMBER}/g' /home/ubuntu/nginx.yml"
        sh 'kubectl create -f /home/ubuntu/nginx.yml'
    }
    }
  }
        
        
