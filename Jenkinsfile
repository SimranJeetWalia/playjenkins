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
  serviceAccountName: jenkins-admin
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
	stage('Push image') {
            steps {
                script {
                	container('radhey') {
                		docker.withRegistry('https://registry.hub.docker.com', 'dockerhubcred') {
                			sampleapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
        }
  stage('Deploy to k8s cluster') {
    steps {
      kubernetesDeploy configs: 'radhey.yml', kubeConfig: [path: ''], kubeconfigId: 'k8s', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
        }
      }
    }
  }
        
        
