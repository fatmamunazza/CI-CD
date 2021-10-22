pipeline {
    environment { 
        registry="fatmamunazza/demo"
        DOCKERHUB_CREDENTIALS=credentials('docker_cred')
        registryCredential = 'docker_cred'
        dockerImage = '' 
    }
   agent any
     tools {
        jdk 'Java_11'
    }
    
   stages {
       stage('build') {
            steps {
               bat 'mvn --version'
               echo 'Building the source'
               bat 'mvn clean compile'
            }
        }
		stage('test') {
            steps {
                echo 'Testing source'
                bat 'mvn test'
            }
        }
		stage('package') {
            steps {
				echo 'packaging demo app'
                bat 'mvn package'
            }
        }
	   stage('Building image') {
	      steps{
	        echo DOCKERHUB_CREDENTIALS_USR
	        script {
	          dockerImage = docker.build(registry)
	        }
	      }
	    }
	    stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }

                } 
            }
        }   
		stage('Cleaning up') { 
            steps { 
                bat "docker rmi fatmamunazza/demo"

            }

        } 

		
    }
}