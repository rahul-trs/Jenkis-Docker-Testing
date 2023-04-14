pipeline {
    agent any 
	stages {
	
	    stage('Clone Repo') {
		  steps {
		    sh 'rm -rf Jenkis-Docker-Testing'	  
	        sh 'git clone https://github.com/rahul-trs/Jenkis-Docker-Testing.git'
			}	
	    }
	
	    stage('Build Docker Image') {
		  steps {
	            sh 'cd /var/lib/jenkins/workspace/pipeline1/Jenkis-Docker-Testing' 
		    sh ' cp /var/lib/jenkins/workspace/pipeline1/Jenkis-Docker-Testing/* /var/lib/jenkins/workspace/pipeline1'
		    sh 'docker build -t rahul9198/pipelinetestdev:v5 .'
		    }
	    }
	
	    stage('Push Image to Docker Hub') {
	      steps {
		    sh    'docker push rahul9198/pipelinetestdev:v5'
	        }
		}
	
	    stage('Deploy to Docker Host') {
		    steps {
		sh 'docker -H tcp://10.0.25.162:2375 rm -f webappdev1'	    
	        sh 'docker -H tcp://10.0.25.162:2375 run --rm -dit -p 9000:80 --name webappdev1 --hostname webappdev1 rahul9198/pipelinetestdev:v5'
	        }
       }
	
	   stage('Check Webapp Reachability') {
		  steps {
		    sh 'sleep 10s'
	        sh 'curl ec2-65-2-83-6.ap-south-1.compute.amazonaws.com:9000'
	        }
	   }
    }
}          
