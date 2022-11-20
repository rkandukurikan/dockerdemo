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
        git branch: 'main', url: 'https://github.com/rkandukurikan/dockerdemo.git'
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
        sh 'docker tag my-webapp ranjithk100/my-webapp:1.0'
      }
    }
    stage ('publish image to dockerhub') {
	 steps {	   
        withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub1')]) {
	sh 'docker login -u ranjithk100 -p ${dockerhub1}'   
}
		sh 'docker push ranjithk100/my-webapp:1.0'
		}
		}
	 //stage('Run Docker container on Jenkins Agent') {
		 //steps {  
			 //sh "docker run -d -p 8003:8080 sunilraju99/my-webapp"         	
                
	
 
      stage ('Run Docker container on Jenkins Agent') {
	      steps {
	     //sh 'docker run -p 8004:8080 -d --name my-webapp ranjithk100/my-webapp:1.0'		      
sshagent(['ubuntu']) {    
sh "ssh -o StrictHostKeyChecking=no ec2-user@44.201.232.171 'docker run -p 8004:8080 -d --name my-webapp ranjithk100/my-webapp:1.0'"
		 
	    }
      }
            
   }
}
}

	
  

    
