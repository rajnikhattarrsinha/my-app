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
}


