pipeline {
  agent any
  stages {
    stage ('test') { // la phase test
steps {
   bat 'gradle test'
   junit 'build/test-results/test/TEST-Matrix.xml'
}
}
}

}
