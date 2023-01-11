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
      stage('Code Analysis') {
    def scannerHome = tool 'SonarQube'
      withSonarQubeEnv('SonarQube') {
      bat """C:\Users\pc\Desktop\S1-SIL\OGL\sonar-scanner-cli-4.6.2.2472-windows\sonar-scanner-4.6.2.2472-windows\bin \
       -D sonar.login=admin \
      -D sonar.password=admin \
     
     -D sonar.projectBaseDir=C:\Users\pc\Desktop\S1-SIL\OGL\TP\TP-8\TP8_jenk \
        -D sonar.projectKey=TP8_jenkins \
        -D sonar.sourceEncoding=UTF-8 \
        -D sonar.language=java \
        -D sonar.sources=TP8_jenkins/src/main \
        -D sonar.tests=TP8_jenkins/src/test \
        -D sonar.host.url=http://localhost:9000/"""
        }
}
}
}

}
