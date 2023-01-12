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
              /*  withSonarQubeEnv(installationName: 'sonar', credentialsId: 'SONARQUBE_TOKEN') {
                bat "./gradle sonarqube \
                  -Dsonar.projectKey=TP8_jenkins \
                  -Dsonar.host.url=http://localhost:9000/ \
                  -Dsonar.login=admin \
                  -Dsonar.projectName=TP8_jenkins \"
                }*/
withSonarQubeEnv('sonar', envOnly: true) {
  // This expands the evironment variables SONAR_CONFIG_NAME, SONAR_HOST_URL, SONAR_AUTH_TOKEN that can be used by any script.
  println "http://localhost:9000/"
}
             
        
}//steps
}//stage
}//stages

}//pipeline
