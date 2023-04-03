pipeline {
    agent any 
   
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
      }
}


        
    
