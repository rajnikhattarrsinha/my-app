node{
   stage('SCM Checkout'){
     git 'https://github.com/rajnikhattarrsinha/my-app'
   }
   stage('Mvn Package'){
      // Get maven home path
      def mvnHome =  tool name: 'Maven 3.5.4', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   stage('Build Docker Image'){
   sh 'docker build -t rajnikhattarrsinha/my-app:2.0.0 .'
   }
   stage('Push Docker Image')
   {
      withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerPWD')]) {
    // some block
         sh "docker login -u rajnikhattarrsinha -p ${dockerPWD}"
         }
      sh 'docker push rajnikhattarrsinha/my-app:2.0.0'
   
   }
   
   stage('Run Container on Deployment-server'){
      def dockerRun= 'docker run -p 8080:8080 -d --name my-app rajnikhattarrsinha/my-app:2.0.0'
      sshagent(['deployserver']) {
    // some block
         sh "ssh -o StrictHostKeyChecking=no root@172.31.86.86 ${dockerRun}"
      }
   }
   
   
}


