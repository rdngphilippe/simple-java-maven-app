pipeline {
  agent any
  stages{    
      stage('Build') {
        steps {
          sh 'mvn -B -DspiTests clean package'
        }
      }
  }
}
