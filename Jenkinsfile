pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('ajish-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t ajishantony2020/python:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push ajishantony2020/python:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
