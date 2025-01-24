pipeline {
  agent any
  stages {


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

  stage('contenerization') {
        steps {
          sh 'echo docker build image'
          sh'echo docker tag image'
          sh'echo docker push image'
          
        }
      }



    stage('Kubernetes Deployment') {
      steps {
        sh 'echo deploy to kubernetes using argoCD'
      }
    }
    stage('integrating testing') {
      steps {
        sh "sleep ${params.SLEEP_TIME}"
        sh 'echo testing using cURL commands z'
      }
    }

  }
  tools {
    maven 'M398'
  }
}
