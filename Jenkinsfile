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
 
       // requires SonarQube Scanner 2.8+
       def scannerHome = tool 'SONAR_RUNNER';
       withSonarQubeEnv('SonarQube') {
            bat "\"${scannerHome}\\bin\\sonar-scanner.bat\""
         
       }//steps

}//code analysis stage
}//stages

}//pipeline
}
