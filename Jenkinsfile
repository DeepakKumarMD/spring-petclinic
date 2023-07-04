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

    stage('Static Analysis') {
      steps {
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Petclinic2 \\
  -Dsonar.projectName=\'Petclinic2\' \\
  -Dsonar.host.url=http://65.1.136.87:9000 \\
  -Dsonar.token=sqp_60f96729b7cd0bbc66026809338d3364d10220ed'''
      }
    }

  }
}