pipeline {
  agent any

  tools {
    maven 'maven3'
  }

  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
      post {
        always {
          junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
        }
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=true'
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts artifacts: 'target/*.war', fingerprint: true
      }
    }
  }
}
