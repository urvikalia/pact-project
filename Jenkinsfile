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
    stage('pre-config') {
      steps {
        sh 'echo \'VIPULanshul27@\' | sudo -S gem install pact_broker-client'
        sh 'pact-broker can-i-deploy'
      }
    }
  }
}