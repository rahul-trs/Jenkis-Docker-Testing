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
            sh 'docker rmi rahul9198/pipelinetest:v1'
		    sh 'docker build -t rahul9198/pipelinetest:v1 .'
		    }
	    }
	
	    stage('Push Image to Docker Hub') {
	      steps {
		    sh    'docker push rahul9198/pipelinetest:v1'
	        }
		}
	
	    stage('Deploy to Docker Host') {
		    steps {
	        sh 'docker -H tcp://10.0.25.162:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 rahul9198/pipelinetest:v1'
	        }
       }
	
	   stage('Check Webapp Reachability') {
		  steps {
		    sh 'sleep 10s'
	        sh 'curl ec2-65-1-147-58.ap-south-1.compute.amazonaws.com:9000'
	        }
	   }
    }
}          
