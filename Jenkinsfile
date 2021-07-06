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
                		docker.withRegistry('https://registry.hub.docker.com', '01fb0ed4-abdb-4190-8873-8f1bb24ac598') {
                			sampleapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
        }
  stage('Deploy to k8s cluster') {
    steps {
      container('radhey') {
      script {
        kubernetesDeploy configs: 'myweb.yaml', dockerCredentials: [[credentialsId: '01fb0ed4-abdb-4190-8873-8f1bb24ac598']], kubeConfig: [path: ''], kubeconfigId: '6c1a4939-baaa-4399-90f4-5bfecf1d84b7', secretName: '', secretNamespace: 'jenkins', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
      }
      }
    }
  }
  }
  }
