pipeline {
  agent any
  stages {
    stage ('test') { // la phase test
steps {
   bat 'gradle test'
   junit 'build/test-results/test/TEST-Matrix.xml'
          cucumber buildStatus: 'UNSTABLE',
                reportTitle: 'My report',
                fileIncludePattern: 'target/*.json',
                trendsLimit: 10
  
}
    }
 stage('Code Analysis') {
   steps{
  
     withSonarQubeEnv() { // Will pick the global server connection you have configured
      bat './gradle sonarqube'
  }

             
        
}//steps
}//stage
}//stages

}//pipeline
