pipeline {
  agent none
  stages {
    stage("Build and Sonar Analysis") {
      agent any
      steps {
        withSonarQubeEnv('sonar_server') {
          sh 'mvn clean package sonar:sonar'
        }
      }
    }
  }
}
