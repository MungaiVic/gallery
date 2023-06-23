pipeline { 
  agent any
  tools { 
    npm "npm"
  }
  stages { 
    stage('clone repository') {
      steps { 
        slackSend (color: '#FFFF00', message: "Clone repository started")
        git 'https://github.com/MungaiVic/gallery'
      }
    }
    stage('Install project dependancies') {
      steps { 
        slackSend (color: '#FFFF00', message: "Install project dependancies started")
        sh 'npm install'
      }
    }
    stage('Tests') {
      steps { 
        slackSend (color: '#FFFF00', message: "Tests started")
        sh 'npm test'

      }
    }
    stage('Deploy to Heroku') {
  steps {
    slackSend (color: '#FFFF00', message: "Deploy to Heroku started")
    withCredentials([usernameColonPassword(credentialsId: 'ip1_heroku', variable: 'HEROKU_CREDENTIALS' )]){
      sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/sleepy-cove-05135.git master'
    }
  }
} 
  }
}