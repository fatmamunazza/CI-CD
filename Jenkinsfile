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
		
    }
}



