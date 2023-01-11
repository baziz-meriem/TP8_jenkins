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
                withSonarQubeEnv(installationName: 'sonar', credentialsId: 'SONARQUBE_TOKEN') {
                bat "./gradle sonarqube \
                  -Dsonar.projectKey=TP8_jenkins \
                  -Dsonar.host.url=http://localhost:9000/ \
                  -Dsonar.login=admin \
                  -Dsonar.projectName=TP8_jenkins \
                  //-Dsonar.projectVersion='1.0'"
                }
             /* node {
              withSonarQubeEnv('My SonarQube Server') {
                 sh 'mvn clean package sonar:sonar'
              }*/
             
        
}//steps
}//stage
}//stages

}//pipeline
