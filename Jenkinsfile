pipeline {
  options {
    disableConcurrentBuilds()
  }
  agent {
    label "jenkins-maven"
  }
  environment {
    CHART_REPOSITORY = "http://192.168.86.24:30001/chartmuseum"
    DEPLOY_NAMESPACE = "jx-prod"
  }
  stages {
    stage('Validate Environment') {
      steps {
        container('maven') {
          dir('env') {
            sh 'jx step helm build'
          }
        }
      }
    }
    stage('Update Environment') {
      when {
        branch 'master'
      }
      steps {
        container('maven') {
          dir('env') {
            // commenting out because we use in-cluster environment-controller
            // sh 'jx step helm apply'
          }
        }
      }
    }
  }
}
