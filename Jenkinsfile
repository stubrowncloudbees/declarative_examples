pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        stash(name: 'build-stash', includes: '**/build/**/*')
      }
    }
    stage('publish') {
      parallel {
        stage('publish junit results') {
          agent any
          steps {
            unstash 'build-stash'
            junit '**/build/test-results/**/*.xml'
          }
        }
        stage('publish artifacts') {
          agent any
          steps {
            unstash 'build-stash'
            archiveArtifacts '**/build/libs/*.jar'
          }
        }
      }
    }
  }
  environment {
    isPublish = true
  }
}