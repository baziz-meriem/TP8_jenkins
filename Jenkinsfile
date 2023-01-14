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
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarQube'
            }

            waitForQualityGate true
          }
        }
       stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
      }
    }
  
    
}//stages

}//pipeline

