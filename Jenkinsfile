pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      parallel {
        stage('Buzz Build') {
          steps {
            echo 'I am a ${BUZZ_NAME}'
            archiveArtifacts(artifacts: '/*.jar', fingerprint: true, allowEmptyArchive: true)
          }
        }

        stage('A') {
          steps {
            echo 'A'
          }
        }

        stage('B') {
          steps {
            echo 'B'
          }
        }

      }
    }

    stage('C') {
      steps {
        echo 'C'
      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}