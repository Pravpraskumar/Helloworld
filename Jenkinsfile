def isValidationSuccess = true
pipeline {
  agent any
  stages {
    stage("Validate") {
        when {
            environment name: 'Run_Setups', value: 'false'
        }
        steps {
            if true{
                isValidationSuccess = false;
            }
        }
    }
    stage('Check Setup') {
      parallel {
        stage('Check Setup') {
          when {
            expression {
              return isValidationSuccess
            }

          }
          steps {
            bat '''
        echo \'Multiline\'                 
        echo \'Example\'                 
        '''
            script {
              env.LOG_FOLDER = "20200313 "
              echo "${env.LOG_FOLDER}"
              echo "${env.Run_Setups}"
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
            def newname="${env.LOG_FOLDER}".trim()
            echo newname
          }

          emailext(to: 'PraveenKumar.Kuppili@Hexagon.com', subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} [${currentBuild.result}]", body: '${FILE, path="C:/DB_Install/logs/'+"${env.LOG_FOLDER}".trim()+'/report.html"}', mimeType: 'text/html')
        }

      }
      steps {
        echo 'Success Stage1pa'
        bat(script: 'test.bat', label: 'test')
      }
    }

  }
  environment {
    Run_Setups = 'false'
  }
}
