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
  - name: jenkinsnode
    image: docker:dind
    securityContext:
      privileged: true
"""
}
}
stages {
	stage('Build Container Builder') {
		steps {
			container('jenkinsnode') {
				script{
					sampleapp = docker.build("simranjeetwalia/sample-app:${env.$BUILD_ID}")
					}
					}
					}
					}
	stage('Depoy to K8s') {
		steps {
			script{
				kubernetesDeploy configs: 'radhey.yml', kubeConfig: [path: ''], kubeconfigId: 'kubeconfig', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://172.31.23.124:6443']
					}
					}
					}
					}
					}
