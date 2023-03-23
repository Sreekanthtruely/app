pipeline {
    agent any
    
    environment{
        registry = "sragro/test"
        registryCredential = 'Dockerhub'
    }
    
    stages{
        stage("build"){
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
            
        }
    }
}
     stage("Publish") {
          steps{
              script {
                  docker.withRegistry( '', registryCredential ) {
                      appimage.push()
                      appimage.push('latest')
                  }
              }
          }
     }
}
