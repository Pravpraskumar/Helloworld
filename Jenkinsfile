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
              mail(to: 'PraveenKumar.Kuppili@hexagon.com', subject: "Automatic DB Setup: ${currentBuild.result}", body: '${readFile(file:"C:\\DB_Install\\report.html")}')
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
          emailext(to: 'info@kitconcept.com', subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} [${currentBuild.result}]", body: "Build URL: ${env.BUILD_URL}.\n\n")
        }

      }
      steps {
        echo 'Success Stage1pa'
      }
    }

  }
}
