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
        sh './gradlew :providers:dropwizard-provider:startScript'
      }
    }
    stage('can-i-deploy') {
      steps {
        sh 'curl -LO https://github.com/pact-foundation/pact-ruby-standalone/releases/download/v1.69.0/pact-1.69.0-osx.tar.gz'
        sleep(time: 40, unit: 'SECONDS')
        sh 'tar xzf pact-1.69.0-osx.tar.gz'
        sh 'cd pact/bin'
        sh './pact-broker version'
      }
    }
  }
}