def isPublish = (env.BRANCH_NAME == 'cloudbees-test') ? 'true' : 'false'

pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh "./gradlew clean build -PisPublish=${isPublish}"
        stash(name: 'build-stash', includes: '**/build/**/*')
      }
    }
    stage('publish') {
      parallel {
        stage('publish junit results') {
          steps {
            unstash 'build-stash'
            junit '**/build/test-results/**/*.xml'
          }
        }
        stage('publish artifacts') {
          steps {
            unstash 'build-stash'
            archiveArtifacts '**/build/libs/*.jar'
          }
        }
      }
    }
  }
}
