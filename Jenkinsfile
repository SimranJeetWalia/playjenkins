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
          kubernetesDeploy(kubeconfigId: '723f7dfb-822b-42b8-9851-9fe1d11961a0',
                 configs: 'myweb.yaml',
                 enableConfigSubstitution: true,
                 dockerCredentials: [
                        [credentialsId: '01fb0ed4-abdb-4190-8873-8f1bb24ac598', url: 'https://registry.hub.docker.com'],
                 ]
)

        }
      }
    }
  }
  }
  }
        
        
