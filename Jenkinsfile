#!groovy

pipeline {

  agent any

  stages {
    stage('Get Contents from Sakura Server') {
      steps {
        sh "google-chrome --headless --disable-gpu --print-to-pdf http://support.sakura.ad.jp/mainte/mainteentry.php?id=24776"
        sh "pdftotext output.pdf output.txt"
      }
    }
  }

  post {
    always {
      script {
        def output = sh(
                        returnStdout: true,
                        script: "cat output.txt | tail -n 50"
                     )

        slackSend message: "Job: ${env.JOB_NAME} with buildnumber ${env.BUILD_NUMBER}\n\n\n\n$output"
        cleanWs()
      }
    }
  }
}
