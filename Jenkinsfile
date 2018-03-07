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
    stage('ws') {
      steps {
        sh 'mvn compile --projects biojava-ws'
        sh 'mvn test --projects biojava-ws'
      }
      post {
        success {
          junit 'biojava-ws/target/surefire-reports/**/*.xml'
        }
      }
    }
    stage('deployment') {
          steps {
            sh 'mvn package --projects biojava-ws'
          }
        }
  }
  post {
    always {
      echo "Send notifications for result: ${currentBuild.result}"
    }
  }
}