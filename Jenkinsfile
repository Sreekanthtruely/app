pipeline {
    agent any 
    # node{
        #label "java_slave"
     
    
    # environment {
        # PATH = "/opt/maven/bin:$PATH"
    
    stages{
        stage("build"){
            steps{
                sh 'mvn clean install'
            }
            
        }
    }

