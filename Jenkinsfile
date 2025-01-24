pipeline {
  agent any
  stages {


    stage('Maven version') {
      steps {
        sh 'mvn -version'
        
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
        sh 'sleep 5s'
        sh 'curl -v --fail --request GET \'http://192.168.192.131:8081/hello\''
      }
    }

  }
  tools {
    maven 'M398'
  }
}
