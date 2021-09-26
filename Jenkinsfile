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
	  withCredentials([string(credentialsId: 'dhub-pass', variable: 'dockerhubpwd')]) {
           sh "docker login -u 966145 -p ${dockerhubpwd}"
		   sh "docker push 966145/myimg:${DOCKER_TAG}"
           }
	    }
	  }
	  stage('Deploy to k8s'){
	    steps{
		  sh "chmod +x changetag.sh"
		  sh "./changetag.sh ${DOCKER_TAG}"
		  sshagent(['kops-machine']){
		    sh "scp -o StrictHostKeyChecking=no pod.yaml ubuntu@172.20.48.127:/home/ubuntu/"
			script{
			    try{
				  sh "ssh ubuntu@172.20.48.127 kubectl apply -f ."				 
				}
				catch(error){
				  sh "ssh ubuntu@172.20.48.127 kubectl create -f ."
				}
			}
			
		  }
		}
	  
	  }
    }

}

def getDockerTag(){
     def tag = sh script: 'git rev-parse HEAD', returnStdout: true
	 return tag
}
