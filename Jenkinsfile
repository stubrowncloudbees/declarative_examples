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
          println("stu")
        }
        
      }
    }
  }
  environment {
    isPublish = true
    BRANCH_NAME = "${env.BRANCH_NAME}"
  }
}