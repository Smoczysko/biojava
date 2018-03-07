pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }
    
  }
  stages {
    stage('setup') {
      steps {
        sh 'mvn clean'
      }
    }
    stage('alignment') {
      parallel {
        stage('alignment') {
          steps {
            sh 'mvn compile'
          }
        }
        stage('') {
          steps {
            sh 'mvn test'
          }
        }
      }
    }
  }
}