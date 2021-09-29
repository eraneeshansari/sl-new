pipeline{
    agent any
stages{
   stage('Build Docker Image')
        {
      steps{
          sh "docker build . -t 966145/japp:${TAG}"
        }
      }
   stage('Push Docker Image')
       { 
     steps{
        withCredentials([string(credentialsId: 'hubpass', variable: 'hpass')]) {
        sh "docker login -u 966145 -p ${hpass}"
        sh "docker push 966145/japp:${currentBuild.number}"
       
}
          
}
      }



}

}

