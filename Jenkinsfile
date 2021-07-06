pipeline {
agent {
    kubernetes {
      label 'cd-jenkins-agent'
      yaml """\
        apiVersion: v1
        kind: Pod
        spec:           
          containers:             
          - name: jenkins-agent
            image: docker:dind
            securityContext:
              privileged: true                           
        """.stripIndent()
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
