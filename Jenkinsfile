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
     script{
       // requires SonarQube Scanner 2.8+
       def scannerHome = tool 'SonarQube Scanner 3.1';
       withSonarQubeEnv('sonar') {
            bat "\"${scannerHome}\\bin\\sonar-scanner.bat\ -Dsonar.projectKey=TP8_jenkins""
         
       }
     }
   }//steps


}//code analysis stage
}//stages

}//pipeline

