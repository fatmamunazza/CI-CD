pipeline {
    environment { 
        registry = "fatmamunazza/demo" 
        DOCKERHUB_CREDENTIALS=credentials('docker_cred')
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
	           bat 'docker build . --tag demo'
	        } 
        }
        stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}
    }
}