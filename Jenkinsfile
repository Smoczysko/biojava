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
        sh 'mvn compile --projects biojava-alignment'
        sh 'mvn test --projects biojava-alignment'
        sh 'mvn site --projects biojava-alignment'
      }
    }
  }
  post {
    always {
      junit 'biojava-*/target/surefire-reports/**/*.xml'
      
    }
    
  }
}