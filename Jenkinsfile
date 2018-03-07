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
        sh 'mvn site --projects biojava-ws'
      }
      post {
        success {
          junit 'biojava-ws/target/surefire-reports/**/*.xml'
          publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'biojava-ws/target/site',
            reportFiles: 'index.html',
            reportName: 'WS Report'
          ]
        }
      }
    }
  }
  post {
    always {
      echo "Send notifications for result: ${currentBuild.result}"
    }
    changed {
      script {
        if (currentBuild.currentResult == 'FAILURE') {
            emailext subject: 'Biojava build failed',
                body: 'Your build has failed!',
                to: 'darkstariw@gmail.com'
        }
      }
    }
  }
}