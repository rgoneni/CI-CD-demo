pipeline {
  agent any
  
  tools
  {
    maven "Maven"
  }
  stages {
    stage ('SCM Checkout') {
      steps {
        //git branch: 'main', 'https://github.com/sunil9999/CI-CD-demo.git'
        git branch: 'main', url: 'https://github.com/sunil9999/CI-CD-demo.git'
      }
      }
    stage ('Excute Maven') {
      steps {
        sh 'mvn package'
      }
    }
    stage ('docker build and tag') {
      steps {
        sh 'docker build -t my-webapp:latest .'
        sh 'docker tag my-webapp sunilraju99/my-webapp:1.0'
      }
    }
    stage ('publish image to dockerhub') {
	 steps {	   
        withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub1')]) {
	sh 'docker login -u sunilraju99 -p ${dockerhub1}'   
}
		sh 'docker push sunilraju99/my-webapp:1.0'
		}
		}
	 //stage('Run Docker container on Jenkins Agent') {
		 //steps {  
			 //sh "docker run -d -p 8003:8080 sunilraju99/my-webapp"         	
                
	
 
      stage ('Run Docker container on Jenkins Agent') {
	     def dockerRun = 'docker run -d -p 8004:8080 -name my-webapp sunilraju99/my-webapp'		      
sshagent(['ubuntu']) {    
sh 'ssh -o StrictHostKeyChecking=no ubuntu@13.233.157.140 $(dockerRun)'
		 
	    }
      }
            
   }


	
  

    
