pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        slackSend(color: '#FFFF00', message: 'Clone repository started :cloud:')
        git 'https://github.com/MungaiVic/gallery'
      }
    }
    stage('Install project dependancies') {
      steps {
        slackSend(color: 'good', message: 'Install project dependancies started :gear: :petri_dish:')
            sh 'npm install'
      }
    }
    stage('Tests') {
      steps {
        slackSend(color: 'good', message: 'Tests started :test_tube:')
            sh 'npm test'
      }
    }
    stage('Deploy to Heroku') {
      steps {
        slackSend(color: 'warning', message: ':airplane_departure: Deploy to Heroku started :rocket:')
        withCredentials([usernameColonPassword(credentialsId: 'ip1_heroku', variable: 'HEROKU_CREDENTIALS')]) {
          sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/sleepy-cove-05135.git master'
        }
      }
    }
  }
  post {
    success {
      slackSend(color: 'good', message: "Build finished successfully :white_check_mark:\nBuild number: ${env.BUILD_NUMBER}\nBuild URL: ${env.BUILD_URL}\nConsole Output: ${env.BUILD_URL}console")
    }
    failure {
      slackSend(color: 'danger', message: "Build ${env.BUILD_NUMBER} failed :x:")
    }
  }
}
