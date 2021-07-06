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


