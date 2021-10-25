pipeline {
    environment { 
        registry="fatmamunazza/demo:$BUILD_NUMBER"
        registryCredential = 'docker_cred'
        dockerImage = '' 
    }
   agent any
     tools {
        jdk 'Java_11'
    }
    
   stages {
       stage('Build') {
            steps {
               bat 'mvn --version'
               echo 'Building the source'
               bat 'mvn clean compile'
            }
        }
		stage('Test') {
            steps {
                echo 'Testing source'
                bat 'mvn test'
            }
        }
		stage('Package') {
            steps {
				echo 'packaging demo app'
                bat 'mvn package'
            }
        }
	   stage('Building image') {
	      steps{
	        script {
	          dockerImage = docker.build(registry)
	        }
	      }
	    }
	    stage('Store image to Dockerhub') { 
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
                bat "docker rmi -f $registry"

            }
        } 
    }
}