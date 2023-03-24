pipeline {
    agent any 
    // using the Timestamper plugin we can add timestamps to the console log
    options {
        timestamps()
    }

    environment {
        //Use Pipeline Utility Steps plugin to read information from pom.xml into env variables
        IMAGE = readMavenPom().getArtifactId()
        VERSION = readMavenPom().getVersion()
    }

    stages {
        stage('Build') {
            steps {
               mvn 'clean install '
            }
            post {
                success {
                    // we only worry about archiving the jar file if the build steps are successful
                    archiveArtifacts(artifacts: '**/target/*.jar', allowEmptyArchive: true)
                }
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
            when {
                branch 'main'  //only run these steps on the master branch
            }
            steps {
                /*
                 * Multiline strings can be used for larger scripts. It is also possible to put scripts in your shared library
                 * and load them with 'libaryResource'
                 */
                sh """
          docker build -t ${IMAGE} .
          docker tag ${IMAGE} ${IMAGE}:${VERSION}
          docker push ${IMAGE}:${VERSION}
        """
            }
        }
    }
}
