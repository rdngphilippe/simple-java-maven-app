pipeline {
  agent any
  environment {
    SONAR_MAVEN_GOAL = 'clean install sonar:sonar'
  }
  stages{    
      stage('Build') {
        steps {
          echo 'Build is running ...'
          sh 'mvn -B -DspiTests clean package'
        }
      }
      stage('SonarQube Analysis'){
        steps{
          withSonarQubeEnv('SonarQube'){
            sh "mvn ${SONAR_MAVEN_GOAL}"
          }
        }
      }
      stage('Test'){
        steps {
        echo 'Test is running'
          sh 'mvn test'
        }
        post {
          always {
            junit 'target/surefire-reports/*.xml'
          }
        }
      }
      stage('Deliver'){
        steps{
          echo 'Deliver is running'
          sh './jenkins/scripts/deliver.sh'
        }
      }
  }
}
