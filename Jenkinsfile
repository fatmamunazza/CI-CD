pipeline {
    environment { 
        registry="fatmamunazza/demo"
        DOCKERHUB_CREDENTIALS=credentials('docker_cred')
        dockerImage = '' 
    }
   agent any
     tools {
        jdk 'Java_11'
    }
    
   stages {
       stage('Login') {
			steps {
				bat 'docker login -u ${DOCKERHUB_CREDENTIALS_USR} -p ${DOCKERHUB_CREDENTIALS_PSW}'	
			}
		}
		stage('package') {
            steps {
				echo 'packaging demo app'
                bat 'mvn install'
            }
        }
        
		stage('Push') {
			steps {
				bat 'docker tag fatmamunazza/demo fatmamunazza/demo'
				bat 'docker push fatmamunazza/demo'
			}
		}
		stage('Cleaning up') { 
            steps { 
                bat "docker rmi fatmamunazza/demo"

            }

        } 

		
    }
}