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
        sh 'pact-broker can-i-deploy -a "Our Consumer" -b http://localhost:9292 --latest'
      }
    }
  }
}