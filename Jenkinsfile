pipeline {
  agent any
  stages {
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
    stage('can-i-deploy') {
      steps {
        sh 'curl -LO https://github.com/pact-foundation/pact-ruby-standalone/releases/download/v1.69.0/pact-1.69.0-osx.tar.gz'
        sh 'tar xzf pact-1.69.0-osx.tar.gz'
        dir(path: 'pact/bin') {
          sh './pact-broker can-i-deploy -a "Our Consumer" -b http://localhost:9292 --latest --retry-while-unknown=12 --retry-interval=12'
        }

      }
    }
    stage('deploy') {
      steps {
        sh 'echo "deploying application"'
      }
    }
  }
}