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
	  
	  //stage('Start test app') {
      //   steps {
      //      powershell """
      //         docker-compose up -d
      //         ./scripts/test_container.ps1
      //      """
      //   }
      //   post {
      //      success {
      //         echo "App started successfully :)"
      //      }
      //      failure {
      //         echo "App failed to start :("
      //      }
      //   }
      //}
      //stage('Run Tests') {
      //   steps {
      //      powershell """
      //         pytest ./tests/test_sample.py
      //      """
      //   }
      //}
      //stage('Stop test app') {
      //   steps {
      //      powershell """
      //         docker-compose down
      //      """
      //   }
      //}
	  stage('Run Anchore') {
               steps {
                  powershell """
                     Write-Output "sahil9604609750/jenkins-course" > anchore_images
                  """
                  anchore bailOnFail: false, bailOnPluginFail: false, name: 'anchore_images'
               }
      }
	  
    }
}
