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
            script {
              env.LOG_FOLDER = "20200313"
              echo "${env.LOG_FOLDER}"
            }

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
          script {
            env.TEST = bat(script:'Call test.bat '+"${currentBuild.result}", label: 'now');
            echo "${env.TEST}"
            def newname="IORDS     "
            echo newname.trim()
          }

          emailext(to: 'PraveenKumar.Kuppili@Hexagon.com', subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} [${currentBuild.result}]", body: '${FILE, path="C:/DB_Install/logs/'+"${env.LOG_FOLDER}"+'/report.html"}', mimeType: 'text/html')
        }

      }
      steps {
        echo 'Success Stage1pa'
        bat(script: 'test.bat', label: 'test')
      }
    }

  }
}
