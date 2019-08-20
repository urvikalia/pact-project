pipeline {
  agent any
  stages {
    stage('InitialState') {
      steps {
        sh 'echo \'Starting pipeline\''
      }
    }
    stage('consumer-check') {
      steps {
        sh './gradlew :consumer:check'
      }
    }
    stage('publish-pact') {
      steps {
        sh './gradlew :consumer:pactPublish'
      }
    }
    stage('provider-verify') {
      steps {
        sh './gradlew :providers:dropwizard-provider:test'
      }
    }
    stage('can-i-deploy') {
      steps {
        sh '''ls
brew info'''
      }
    }
  }
}