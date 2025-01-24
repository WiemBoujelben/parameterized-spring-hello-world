pipeline {
  agent any
  stages {


    stage('Maven version') {
      steps {
        sh 'mvn -version'
        sh "echo Sleep Time -${params.SLEEP_TIME} port number - ${params.APP_PORT} branch - ${params.BRANCH}"
        
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean install'
        archiveArtifacts 'target/spring-boot-*.jar'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
        junit(testResults: 'target/surefire-reports/TEST-*.xml', keepProperties: true, keepTestNames: true)
      }
    }

  stage('Local deployment ') {
        steps {
          sh """java -jar target/spring-boot-*.jar > /dev/null &"""
          
          
        }
      }



  
    stage('integrating testing') {
      steps {
        sh "sleep ${params.SLEEP_TIME}"
        sh "curl -v --fail --request GET \'http://192.168.192.131:${params.APP_PORT}/hello'"
      }
    }

  }
  tools {
    maven 'M398'
  }
}
