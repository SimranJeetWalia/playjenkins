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
          kubernetesDeploy(kubeconfigId: '47027e6b-c4ae-43c0-a916-a9b5e16f0c3e',
                 configs: 'myweb.yaml',
                 enableConfigSubstitution: true,
                 secretNamespace: 'jenkins',
                 secretName: 'jenkins',
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
        
        
