pipeline {
  agent {
          label 'my-pod'
  }
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
          if (env.BRANCH_NAME == 'madster'){
            isPublish = true
          }
        }
        
        sh 'echo $isPublish'
      }
    }
  }
  environment {
    isPublish = false
  }
}
