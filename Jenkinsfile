pipeline {
  agent any 
  environment{
    DOCKER_TAG = getDockerTag()
  }
  stages{
      stage('Build Docker Image'){
	      steps{
		     sh "docker build . -t 966145/myimg:${DOCKER_TAG}"
		  }
	  
	  }
	stage('DockerHub Push'){
	  steps{
	  withCredentials([string(credentialsId: 'docker-hub', variable: 'dhub-pass')]) {
           sh "docker login -u 966145 -p ${dhub-pass}"
		   sh "docker push 966145/myimg:${DOCKER_TAG}"
           }
	    }
	  }
    }

}

def getDockerTag(){
     def tag = sh script: 'git rev-parse HEAD', returnStdout: true
	 return tag
}
