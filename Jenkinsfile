pipeline {
  environment {
    registry = 'chyuan530/devops'
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/chyuan530/devops-proj1.git', branch: 'main', credentialsId: ''])
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ':$BUILD_NUMBER'
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry('', registryCredential ) {
             dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}
