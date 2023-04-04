pipeline {
  environment {
    imagename = "sragro/new-app"
    registryCredential = 'Dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Build') {
        steps {
            sh 'mvn clean install '
	      
            }
        }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')
          }
        }
      }
    }
  }
}
  
        
    
