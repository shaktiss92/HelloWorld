pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      steps {
        echo 'I am a ${BUZZ_NAME}'
        archiveArtifacts(artifacts: '/*.jar', fingerprint: true, allowEmptyArchive: true)
      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}