pipeline {
    agent any 
   
      stages {
          stage('Build') {
             steps {
               sh 'mvn clean install '
	       sh "mv target/*.war target/myweb.war"
            }
        }
           stage('Quality Analysis') {
            
                // run Sonar Scan and Integration tests in parallel. This syntax requires Declarative Pipeline 1.2 or higher
               
                 //run this stage on any available agent
                   steps {
                       sh 'mvn test'
                    }
	   }
	      stage('Deploy') {
		      steps {
			      sh """
                              scp -o StrictHostKeyChecking=no target/myweb.war  
                              ec2-user@43.205.237.51 /opt/tomcat/webapps/
                              ssh ec2-user@43.205.237.51 /opt/tomcat/bin/shutdown.sh
                              ssh ec2-user@43.205.237.51 /opt/tomcat/bin/startup.sh
                              """
		      }
	      }
	      
      }
}


        
    
