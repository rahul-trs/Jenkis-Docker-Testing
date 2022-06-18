pipeline {
    agent any 
	stages {
	
	    stage('Clone Repo') {
		    steps {
		      sh 'rm -rf dockertest1'
	        sh 'git clone https://github.com/rahul-trs/dockertest1.git'
			    }	
	    }
	
	    stage('Build Docker Image') {
		    steps {
	        sh 'cd /var/lib/jenkins/workspace/pipeline1/dockertest1'
		      sh ' cp /var/lib/jenkins/workspace/pipeline1/dockertest1/* /var/lib/jenkins/workspace/pipeline1'
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
	        sh 'docker -H tcp://10.1.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 rahul9198/pipelinetest:v1'
	        }
      }
	
	    stage('Check Webapp Reachability') {
		    steps {
		      sh 'sleep 10s'
	        sh 'curl ec2-54-174-124-118.compute-1.amazonaws.com:9000'
	        }
      }
}          
