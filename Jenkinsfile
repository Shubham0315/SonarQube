pipeline {
  agent none
  stages {
    stage("Build and Sonar Analysis") {
      agent any
      steps {
        withSonarQubeEnv('SonarQube') {
          sh 'mvn clean package sonar:sonar'
        }
      }
    }
  }
}
