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
             
                sh 'mvn clean package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                //sh 'docker build -t samplewebapp:latest .' 
                //sh 'docker tag samplewebapp:latest jeevankiran/samplewebapp:latest'
		sh 'docker build -t samplewebapp:V1 .' 
                sh 'docker tag samplewebapp:V1 jeevankiran/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
          // sh  'docker push jeevankiran/samplewebapp:latest'
          sh  'docker push jeevankiran/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 jeevankiran/samplewebapp"
 
            }
        }
 //stage('Run Docker container on remote hosts') {
             
            //steps {
                //sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 jeevankiran/samplewebapp"
 
           // }
      //  }
    }
	}
    
