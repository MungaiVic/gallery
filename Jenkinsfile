pipeline {
  agent any
  stages {
    stage('clone repository') {
      steps {
        slackSend(color: '#FFFF00', message: 'Clone repository started')
        git 'https://github.com/MungaiVic/gallery'
      }
    }
    stage('Install project dependancies') {
      steps {
        slackSend(color: 'good', message: 'Install project dependancies started')

            sh 'npm install'
      }
    }
    stage('Tests') {
      steps {
        slackSend(color: 'good', message: 'Tests started')

            sh 'npm test'
      }
    }
    stage('Deploy to Heroku') {
      steps {
        slackSend(color: 'warning', message: 'Deploy to Heroku started :rocket:')
        withCredentials([usernameColonPassword(credentialsId: 'ip1_heroku', variable: 'HEROKU_CREDENTIALS')]) {
          sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/sleepy-cove-05135.git master'
        }
      }
    }
  }
  post {
    success {
      slackSend(color: 'good', message: "Build finished successfully :white_check_mark:\nBuild number: ${env.BUILD_NUMBER}\nBuild URL: ${env.BUILD_URL}\nConsole Output: ${env.BUILD_URL}console\nChanges: ${env.CHANGE_URL}")
    }
    failure {
      slackSend(color: 'danger', message: 'Build failed :x:')
    }
  }
}
