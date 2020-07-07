pipeline {
  agent any
  stages {
    stage('Check Setup') {
      parallel {
        stage('Parcheck'){
          stages{
            stage('Check Setup') {
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
        stage('test Parallel-1'){
          parallel{
            stage('test-inner-1'){
              steps {
                echo 'Nested Parallel intest-1'
              }
            }
            stage('test-inner-2'){
              steps {
                echo 'Nested Parallel intest-2'
              }
            }
          }
        }
         stage('test Parallel-2'){
            steps {
              echo 'Nested Parallel test'
            }
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
