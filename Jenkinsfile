pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      steps {
        echo 'Placeholder'
        archiveArtifacts(artifacts: '/*.jar', fingerprint: true, allowEmptyArchive: true)
      }
    }

  }
}