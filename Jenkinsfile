pipeline {
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
	                    dockerImage = docker.build(registry)
	                }
	            } 
        }
    }
}