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
