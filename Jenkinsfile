pipeline {
    environment { 
        registry = "fatmamunazza/demo" 
        DOCKERHUB_CREDENTIALS=credentials('docker_cred')
        DOCKERHUB_CREDENTIALS_PSW="sapient123"
        DOCKERHUB_CREDENTIALS_USR="fatmamunazza"
        dockerImage = '' 
    }
   agent any
     tools {
        jdk 'Java_11'
    }
    
   stages {
       stage('Login') {
			steps {
				bat 'echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin'	
			}
		}
		stage('package') {
            steps {
				echo 'packaging demo app'
                bat 'mvn install'
            }
        }
        stage('Building Our Image') { 
	        steps { 
	           bat 'docker build -t fatmamunazza/demo .'
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