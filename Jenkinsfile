pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh '''./mvnw clean compile
'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

  }
}