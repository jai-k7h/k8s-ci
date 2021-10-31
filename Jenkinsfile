
pipeline {


  environment {
    registry = "registry.hub.docker.com/vadar/nginx"
    dockerImage = ""
    ImageName = "${registry}:${BUILD_NUMBER}"
  }
  agent master
  stages {

    stage('Checkout Source') {
      steps {
        git branch: 'main', credentialsId: '8b6b6a7e-add0-427a-9fc6-04a3ff149eda', url: 'https://github.com/jai-k7h/k8s-ci/'
      }
    }

    stage('Build image') {  
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry('registry.hub.docker.com/vadar/nginx') {
            sh "docker login -u vadar -p qwer1234A nexus.skssteels.tk:8083"
            sh 'docker push ${registry}:${BUILD_NUMBER}'
          }
        }
      }
    }
  }

}
