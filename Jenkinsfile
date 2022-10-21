pipeline{
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
     environment {
         DOCKERHUB_CREDENTIALS = credentials('docker-hub1')
     }
     stages {
      stage('build') {
          steps{
            sh 'docker build -t nireimage/dp-alpine:latest .'
          }
      }
      stage('Login') {
          steps{
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
          }
      }
      stage('push') {
          steps {
            sh 'docker push nireimage/dp-alpine:latest'
          }
      }
    }
    post {
      always {
        sh 'docker logout'  
      }
    }
 }
