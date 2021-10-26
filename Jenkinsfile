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
     stage('Building image') {
	      steps{
	        script {
	          dockerImage = docker.build(registry)
	          echo dockerImage
	          bat "docker tag fatmamunazza/demo:$BUILD_NUMBER fatmamunazza/demo:latest"
	        }
	      }
	    }
       
    }
}