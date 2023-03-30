pipeline {
    agent any 
    
    environment {
        //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
        registry = "sragro/test"
        registryCredential = 'Dockerhub'
    }

    stages {
        stage('Build') {
            steps {
               mvn 'clean install '
            }
        }
        stage('Quality Analysis') {
            
                // run Sonar Scan and Integration tests in parallel. This syntax requires Declarative Pipeline 1.2 or higher
               
                 //run this stage on any available agent
                    steps {
                        mvn 'test'
                    }
                
        }

        stage('Build and Publish Image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    docker.withRegistry('',registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
    
