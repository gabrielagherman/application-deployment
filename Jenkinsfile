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
     
//       stage('Run Docker container on Jenkins Agent') {
             
//             steps 
// 			{
//                 sh "docker run -d -p 8003:8080 gabrielagherman/samplewebapp"
 
//             }
//         }
 
	// stage("Git Checkout"){
	//	 steps{
	//		 sh 'pwd'
	//		 sh 'git clone https://github.com/gabrielagherman/application-deployment.git'
	//	 	 sh 'pwd'
	//	 }
	 //}
	 stage ("Run ansible playbook on remote hosts")
	 {
		 steps{
			//sh 'cd /var/lib/jenkins/workspace/auto-deploy/application-deployment'
			sh 'cd /etc/ansible'
			sh 'pwd'
			//ansiblePlaybook (credentialsId: 'credentialeptmasina', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/inventory', playbook: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/playbook.yaml')
		 	//ansiblePlaybook credentialsId: 'credentialeptmasina', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/inventory', playbook: '/var/lib/jenkins/workspace/auto-deploy/application-deployment/playbook.yaml'
			sh 'sudo ansible-playbook ./application-deployment/playbook.yaml -i ./application-deployment/inventory --key-file ./application-deployment/aws-key.pem'
			 //ansiblePlaybook credentialsId: 'credentialeptmasina', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/inventory', playbook: '/etc/ansible/playbooktest.yaml'
		 }
	 }
	 
	 
	 
 // stage('Run Docker container on remote hosts') {
             
   //         steps {
		//withAWS(credentials: 'credentiale-masina', region: 'eu-central-1'){
		//sshagent(['credentials']) {
		   // sh "ssh -tt ubuntu@3.71.176.233" 
	//	    sh "ssh ubuntu@3.71.176.233 docker run -d -p 8003:8080 gabrielagherman/samplewebapp"
		   
		   // sh "docker run -d -p 8003:8080 gabrielagherman/samplewebapp"
		//}
            //}
        
   // }
	}
}
