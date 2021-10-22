pipeline {
    environment { 
        registry = "fatmamunazza/demo" 
        DOCKERHUB_CREDENTIALS_PSW="sapient123"
        DOCKERHUB_CREDENTIALS_USR="fatmamunazza"
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
        stage('Building Our Image') { 
	        steps { 
	           script { 
                    dockerImage = docker build -t registry + ":$BUILD_NUMBER" . 
                }
	        } 
        }
        stage('Login') {

			steps {
				bat 'docker login -u fatmamunazza'
			}
		}
		stage('Push') {

			steps {
				bat 'docker push fatmamunazza/demo:latest'
			}
		}
		stage('Cleaning up') { 
            steps { 
                bat "docker rmi $registry:$BUILD_NUMBER" 

            }

        } 

		
    }
}