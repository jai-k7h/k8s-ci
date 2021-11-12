
pipeline {


  environment {
    registry = "registry.hub.docker.com/jaik7/tvr-configurator-ui"
    dockerImage = ""
    ImageName = "${registry}:${BUILD_NUMBER}"
  }
  agent any
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
          sh '''docker build -t docker1-tag:latest us.gcr.io/project-name/docker1-tag:latest -f "Dockerfile1" .'''
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry('registry.hub.docker.com/vadar/nginx', 'docker-cred') { 
            sh "docker login -u ${USERNAME} -p ${PASSWORD}"
            sh 'docker push ${registry}:${BUILD_NUMBER}'
          }
        }
      }
    }
  }

}
