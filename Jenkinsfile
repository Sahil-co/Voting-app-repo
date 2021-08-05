@Library('github.com/Sahil-co/demo-shared-pipeline') _

pipeline {
  agent any
  stages {
    stage('Call Library Hello-World Function') {
      steps {
        script {
          helloWorld()
        }
      }
    }
  }
}