pipeline{
    agent any
    
stages{
   stage('Build Docker Image')
        {
      steps{
          sh "docker build -t 966145/japp:v1 ."
        }
      }



}

}

def gittag() {
      def tag = sh script: 'git rev-parse HEAD', returnStdOut: true
      return tag

}
