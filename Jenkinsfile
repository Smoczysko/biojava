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
      steps {
        sh 'mvn compile'
        sh 'mvn test'
      }
    }
  }
}