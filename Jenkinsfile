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
    stage('provider-test') {
      steps {
        sh './gradlew :providers:dropwizard-provider:test'
      }
    }
    stage('dummy-deploy') {
      steps {
        sh 'echo "provider deployed "'
      }
    }
  }
}