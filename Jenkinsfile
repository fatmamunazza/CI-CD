pipeline {
   agent any
     tools {
        jdk 'Java_11'
    }
   stages {
        stage('build') {
            steps {
               sh 'mvn --version'
               echo 'Building the source'
               sh 'mvn clean compile'
            }
        }
		stage('test') {
            steps {
                echo 'Testing source'
                sh 'mvn test'
            }
        }
		stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
		stage('package') {
            steps {
				echo 'packaging testapp'
                bat 'mvn package'
            }
        }
    }
}



