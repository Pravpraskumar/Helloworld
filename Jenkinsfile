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
        for /f "tokens=1* delims=" %%a in (\'date /T\') do set datestr=%%a                 
        cd C:\\\\DB_Install\\\\logs                 
        set foname=%datestr:~10,4%%datestr:~4,2%%datestr:~7,2%                 
        mkdir %foname%                 
        if exist "C:\\\\DB_Install\\\\lsDB.txt" (set /p oldContent=<C:\\\\DB_Install\\\\lsDB.txt) else exit(1)
        xcopy C:\\\\DB_Install\\\\lsDB.txt C:\\\\DB_Install\\\\logs\\\\%foname%\\\\oldSetup.txt* /Y                 
        set oldBuildno=%oldContent:~10,-4%                 
        echo %oldBuildno%                                  
        if exist "\\\\\\\\azdord-fs\\\\DeliveryQA\\\\10.0\\\\SP\\\\DB\\\\lastSetup.txt" ( xcopy \\\\\\\\azdord-fs\\\\DeliveryQA\\\\10.0\\\\SP\\\\DB\\\\lastSetup.txt C:\\\\DB_Install\\\\lsDB.txt* /Y )
        set /p newContent=<C:\\\\DB_Install\\\\lsDB.txt
        set newBuildno=%newContent:~10,-4%
        echo %newBuildno% 
        if(newBuildno NEQ oldBuildno) newSetup=true
        echo %newSetup%                 
        if(%newSetup% EQU true) echo \'NewSetup Obtained\' else exit(1)
        '''
          }
        }

        stage('Stage1Pa') {
          post {
            always {
              mail(to: 'PraveenKumar.Kuppili@hexagon.com', subject: "Automatic DB Setup: ${currentBuild.result}", body: ${FILE, path="C:\\DB_Install\\report.html"})
            }

          }
          steps {
            echo 'Stage Parallel'
          }
        }

      }
    }

    stage('Stage-3') {
      steps {
        echo 'Success Stage1pa'
      }
    }

  }
}
