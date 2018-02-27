pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        stash(name: 'build-stash', includes: '**/**')
        sh "echo ${BRANCH_NAME}"
      }
    }
    stage('publish') {
      parallel {
        stage('publish junit results') {
          agent any
          steps {
            unstash 'build-stash'
          }
        }
        stage('publish artifacts') {
          agent any
          steps {
            unstash 'build-stash'
          }
        }
      }
    }
    stage('Yes or no') {
      agent any
      steps {
        script {
          if (env.BRANCH_NAME == 'master'){
            isPublish = true
          }
        }
        
      }
    }
  }
  environment {
    isPublish = false
  }
}