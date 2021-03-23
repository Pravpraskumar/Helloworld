pipeline {
  agent any
  stages {
    stage('test Parallel-2'){
            steps {
              echo 'Nested Parallel test'
            }
    }
     stage('Stage1Pa') {
          steps {
            echo 'Stage Parallel'
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

          emailext(to: 'PraveenKumar.Kuppili@Hexagon.com; Shraddha.Kulkarni@Hexagon.com', subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} [${currentBuild.result}]", body: 'test'+"${env.LOG_FOLDER}".trim()+'/report.html"}', mimeType: 'text/html')
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
