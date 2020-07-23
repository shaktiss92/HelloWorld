pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      parallel {
        stage('Buzz Build') {
          steps {
            echo 'I am a ${BUZZ_NAME}'
            archiveArtifacts(artifacts: '/*.jar', fingerprint: true, allowEmptyArchive: true)
            stash(name: 's3', allowEmpty: true, includes: '**')
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
        unstash 's3'
        echo 'C'
      }
    }

    stage('Input') {
      steps {
        input(message: 'Wait', ok: 'Yes')
      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}