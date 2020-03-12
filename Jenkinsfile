pipeline {
  agent any
  stages {
    stage('Check Setup') {
      parallel {
        stage('Check Setup') {
          steps {
            bat '''
        echo \'Multiline\'                 
        echo \'Example\'                 
        '''
          }
        }

        stage('Stage1Pa') {
          steps {
            echo 'Stage Parallel'
          }
        }

      }
    }

    stage('Stage-3') {
      post {
        always {
          emailext(to: 'PraveenKumar.Kuppili@Hexagon.com', subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} [${currentBuild.result}]", body: '''<pre>
          ${FILE, path="C:/DB_Install/report.html"}
          </pre>''', mimeType: 'text/html')
        }

      }
      steps {
        echo 'Success Stage1pa'
      }
    }

  }
}