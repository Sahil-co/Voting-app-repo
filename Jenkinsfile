pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
	  stage('Docker Build') {
         steps {
            bat 'docker images -a'
            bat """
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """
         }
      }
	  
	  stage('Start test app') {
         steps {
            powershell """
               docker-compose up -d
               ./scripts/test_container.ps1
            """
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            powershell """
               pytest ./tests/test_sample.py
            """
         }
      }
      stage('Stop test app') {
         steps {
            powershell """
               docker-compose down
            """
         }
      }
	  stage('Run Trivy') {
               steps {
                  //sleep(time: 30, unit: 'SECONDS')
                  powershell """
                  C:\\Windows\\System32\\wsl.exe -- sudo trivy sahil9604609750/jenkins-course
                  """
               }
      }
    }
}
