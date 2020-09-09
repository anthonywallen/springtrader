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

    stage("Deploy to Staging") {
      agent {
        label "lead-toolchain-skaffold"
      }
      when {
          branch 'master'
      }
      environment {
        ISTIO_DOMAIN = "${env.stagingDomain}"
        PRODUCT_NAME = "${env.product}"
      }
      steps {
        container('skaffold') {
          unstash 'build'
          sh "skaffold deploy -a image.json -n ${env.stagingNamespace}"
          stageMessage "Successfully deployed to staging:\nspringtrader-${env.product}.${env.stagingDomain}/spring-nanotrader-web/"
        }
      }
    }

    // Note: Add gating stage here

    // Note: Add prod stage here

  }
}