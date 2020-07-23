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
      when {
        branch 'master'
      }
      steps {
        input(message: 'Wait', ok: 'Yes')
      }
    }

    stage('DeployStage') {
      post {
        success {
          emailext(subject: 'Completed: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\'', body: '<p>COMPLETED: Job \'${env.JOB_NAME} [${env.GIT_BRANCH}]\':</p>')
        }

        failure {
          emailext(subject: 'FAILED: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\'', body: '<p>FAILED: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\':</p>')
        }

      }
      steps {
        echo 'deploy.sh ${env.GIT_COMMIT}'
      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}