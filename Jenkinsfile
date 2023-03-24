pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
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
                sh 'docker tag samplewebapp gabrielagherman/samplewebapp:latest'
                //sh 'docker tag swebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "docker-cred", url: "" ]) {
          sh  'docker push gabrielagherman/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 gabrielagherman/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
		withAWS(credentials: 'Jenkins', region: 'eu-central-1'){
		sh "docker -H ssh -i aws-key.pem ubuntu@3.75.171.17 run -d -p 8003:8080 gabrielagherman/samplewebapp"
		}
            }
        }
    }
	}
    
