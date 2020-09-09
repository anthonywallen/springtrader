pipeline {
  agent any
  stages {

    // Note: Add build stage here

    stage('Build') {
      agent {
        label "lead-toolchain-skaffold"
      }
      steps {
        container('skaffold') {
          sh "skaffold build --file-output=image.json"
          stash includes: 'image.json', name: 'build'
          sh "rm image.json"
        }
      }
    }

    // Note: Add deploy stage here

    // Note: Add gating stage here

    // Note: Add prod stage here

  }
}