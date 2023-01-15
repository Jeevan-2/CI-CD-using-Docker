pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/Jeevan-2/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp:latest Jeevan-2/project:latest'
                //sh 'docker tag samplewebapp:latest Jeevan-2/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dock", url: "" ]) {
          sh  'docker push Jeevan-2/project:latest'
        //  sh  'docker push Jeevan-2/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 Jeevan-2/project"
 
            }
        }
 //stage('Run Docker container on remote hosts') {
             
            //steps {
                //sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 Jeevan-2/samplewebapp"
 
           // }
      //  }
    }
	}
    
