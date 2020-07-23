pipeline {
  agent any
  stages {
    stage('BuildStage') {
      parallel {
        stage('Build Talend') {
          steps {
            echo 'talend_build.zip'
            archiveArtifacts(artifacts: '/*.jar', fingerprint: true, allowEmptyArchive: true)
            stash(name: 's3_stash', allowEmpty: true, includes: '**')
          }
        }

        stage('Build Java') {
          steps {
            echo 'java_build.sh'
          }
        }

        stage('Build Scala') {
          steps {
            echo 'scala_build.sh'
          }
        }

      }
    }

    stage('TestStage') {
      steps {
        unstash 's3_stash'
        echo 'Test all build steps'
      }
    }

    stage('WaitForInput') {
      steps {
        input(message: 'Wait', ok: 'Yes')
      }
    }

    stage('DeployStage') {
      steps {
        echo 'deploy.sh'
      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}