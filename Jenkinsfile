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
        sh 'docker tag my-webapp rgoneni/my-webapp:1.0'
      }
    }
    stage ('publish image to dockerhub') {
	 steps {	   
        //withCredentials([string(credentialsId: 'id_hubdocker', variable: 'dockerhub1')]) {
		 docker.withRegistry('https://registry.hub.docker.com', 'id_hubdocker') {
	//sh 'docker login -u sunilraju99 -p ${}'   
}
		//sh 'docker push rgoneni/my-webapp:1.0'
	    def customImage = docker.build("rgoneni/my-webapp:1.0")
		customImage.push()
		}
		}
	 //stage('Run Docker container on Jenkins Agent') {
		 //steps {  
			 //sh "docker run -d -p 8003:8080 sunilraju99/my-webapp"         	
                
	
 
      stage ('Run Docker container on Jenkins Agent') {
	      steps {
	     //sh 'docker run -p 8004:8080 -d --name my-webapp sunilraju99/my-webapp:1.0'		      
//sshagent(['ubuntu']) {    
//sh "ssh -o StrictHostKeyChecking=no ubuntu@13.233.157.140 'docker run -p 8004:8080 -d --name my-webapp sunilraju99/my-webapp:1.0'"
	script {
	sh 'docker run --rm -p 8004:8080 -d --name my-webapp rgoneni/my-webapp:1.0	 
	    }
      }
            
   }
}
}

	
  

    
