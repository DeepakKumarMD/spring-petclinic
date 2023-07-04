pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('Compile') {
      steps {
        sh '''./mvnw clean compile
'''
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Petclinic1 \\
  -Dsonar.projectName=\'Petclinic1\' \\
  -Dsonar.host.url=http://13.233.5.63:9000 \\
  -Dsonar.token=sqp_d5b00a89b5076394d62cc3ab0f9d76ac0a7effd8'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh './mvnw spring-boot:run </dev/null &>/dev/null &'
          }
        }

        stage('Integration and Perfomance Test') {
          steps {
            sh './mvnw verify'
            junit '**/target/surefire-reports/'
            perfReport '**/target/jmeter/results/*'
          }
        }

      }
    }

  }
}