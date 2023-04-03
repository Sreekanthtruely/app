pipeline {
    agent any 
   environment {
        DATE = new Date().format('yy.M')
        TAG = "${DATE}.${BUILD_NUMBER}"
    stages {
        stage('Build') {
            steps {
               sh 'mvn clean install '
            }
        }
        stage('Quality Analysis') {
            
                // run Sonar Scan and Integration tests in parallel. This syntax requires Declarative Pipeline 1.2 or higher
               
                 //run this stage on any available agent
                    steps {
                       sh 'mvn test'
                    }
        }
        stage('Docker Build') {
            steps {
                script {
			sh 'docker build -t sragro/New-world:${TAG} .'
                }
            }
        }
	    stage('Pushing Docker Image to Dockerhub') {
            steps {
                script {
                 sh """   docker.withRegistry('https://registry.hub.docker.com', 'Dockerhub') 
                        docker.image("sragro/New-world:${TAG}").push()
                        docker.image("sragro/New-world:${TAG}").push("latest")
			sh """
                    }
                }
            }
        }
    }
}



        
    
