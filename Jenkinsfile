pipeline {
agent {
    kubernetes {
      yaml """\
        apiVersion: v1
        kind: Pod
        metadata:
          labels:
            name: simranjeet
        spec:           
          containers:             
          - name: simranjeet
            image: docker:dind
            securityContext:
              privileged: true                           
        """.stripIndent()
    }
  }
stages {
        stage('Build Container Builder') {
                steps {
                        container('simranjeet') {
                                script{
                                        sampleapp = docker.build("simranjeetwalia/sample-app:${env.$BUILD_ID}")
                                        }
                                        }
                                        }
                                        }
                                        }
                                        }
