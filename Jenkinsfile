pipeline {
  agent any

  tools {
    jdk 'JDK17'     // Use the exact name from Jenkins tools config
    maven 'Maven3'  // Use the exact name from Jenkins tools config
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install Dependencies') {
      steps {
        script {
          if (isUnix()) {
            sh 'mvn clean install'
          } else {
            bat 'mvn clean install'
          }
        }
      }
    }
    stage('Build & Test') {
      steps {
        script {
          if (isUnix()) {
            sh 'mvn package'
            sh 'mvn test'
          } else {
            bat 'mvn package'
            bat 'mvn test'
          }
        }
      }
    }
    stage('Archive Artifact') {
      steps {
        junit 'target/surefire-reports/*.xml'
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }
    }
  }
}

