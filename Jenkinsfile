pipeline {
  agent any
  stages {
    stage ('test') { // la phase test
            post {
        failure {
          script {
            mail= " test terminé avec échec "
          }

        }

        success {
          script {
            mail=" test terminé avec succès "
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
    
    
     
        stage('Code Analysis') {
                post {
        failure {
          script {
            mail= " Code Analysis terminé avec échec "
          }

        }

        success {
          script {
            mail=" Code analysis terminé avec succès "
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
       stage('Build') {
               post {
        failure {
          script {
            mail= " Build terminé avec échec "
          }

        }

        success {
          script {
            mail=" Build terminé avec succès "
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
    
        stage('Deployment') {
                post {
        failure {
          script {
            mail= " Deployement terminé avec échec "
          }

        }

        success {
          script {
            mail=" Deployement terminé avec succès "
          }

        }

      }
      steps {
        bat 'gradle publish'
      }
    }
        stage('Mail Notification') {
      steps {
        mail(subject: 'TP JenkinsOGL notification', body: mail, cc: 'jm_baziz@esi.dz' ,bcc:'jm_baziz@esi.dz')
      }
    }
  
    
}//stages

}//pipeline

