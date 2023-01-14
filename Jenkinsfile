pipeline {
  agent any
  stages {
    stage ('test') { // la phase test
            post {
        failure {
          script {
            mail= " Test phase failed "
          }

        }

      }
steps {
   bat 'gradle test'
   junit 'build/test-results/test/TEST-Matrix.xml'
          cucumber buildStatus: 'UNSTABLE',
                reportTitle: 'My report',
                fileIncludePattern: 'target/*.json',
                trendsLimit: 10
  
}
    }
            stage('Mail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jm_baziz@esi.dz' ,bcc:'jm_baziz@esi.dz')
      }
    }
    
     
        stage('Code Analysis') {
                post {
        failure {
          script {
            mail= " Code Analysis phase failed "
          }

        }

      }
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarQube'
            }

            waitForQualityGate true
          }
        }
            stage('Mail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jm_baziz@esi.dz' ,bcc:'jm_baziz@esi.dz')
      }
    }
       stage('Build') {
               post {
        failure {
          script {
            mail= " Build phase failed "
          }

        }

      }
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
      }
    }
            stage('Mail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jm_baziz@esi.dz' ,bcc:'jm_baziz@esi.dz')
      }
    }
    
        stage('Deployment') {
                post {
        failure {
          script {
            mail= " Deployement phase failed "
          }

        }

        success {
          script {
            mail=" Deployement phase ended successfully "
          }

        }

      }
      steps {
        bat 'gradle publish'
      }
    }
        stage('Mail Notification') {
      steps {
        mail(subject: 'TPOGL Jenkins notification', body: mail, cc: 'jm_baziz@esi.dz' ,bcc:'jm_baziz@esi.dz')
      }
    }
  
    
}//stages
  environment {
    mail = ''
  }
}//pipeline

