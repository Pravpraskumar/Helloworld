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
          post {
            always {
              mail(to: 'PraveenKumar.Kuppili@hexagon.com', subject: "Automatic DB Setup: ${currentBuild.result}", body: readFile(file:"C:\\DB_Install\\report.html"))
            }

          }
          steps {
            echo 'Stage Parallel'
          }
        }

      }
    }

    stage('Stage-3') {
      post {
        always {
          emailext(body: '''<pre>
${FILE, path="C:/Program Files (x86)/Jenkins/workspace/Unit test Result Mailer/report.html"}
</pre>''', mimeType: 'text/html', subject: "[Jenkins] ${jobName}", to: 'PraveenKumar.Kuppili@Hexagon.com')
        }

      }
      steps {
        echo 'Success Stage1pa'
      }
    }

  }
}