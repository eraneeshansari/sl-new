pipeline{
    agent any
    environment {
           TAG = gittag()
               } 
stages{
   stage('Build Docker Image')
        {
      steps{
          sh "docker build -t 966145/japp:${TAG} ."
        }
      }



}

}

def gittag() {
      def tag = sh script: 'git rev-parse HEAD', returnStdOut: true
      return tag

}
