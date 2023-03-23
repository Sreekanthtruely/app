pipeline {
    agent any
    
    stages{
        stage("build"){
            steps{
                sh 'mvn clean install'
            }
            
        }
    }
}
     stage('Publish') {
          environment {
              registryCredential = 'dockerhub'
          }
          steps{
              script {
                  def appimage = docker.build registry + ":$BUILD_NUMBER"
                  docker.withRegistry( '', registryCredential ) {
                      appimage.push()
                      appimage.push('latest')
                  }
              }
          }
      
