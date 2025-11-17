pipeline {
 agent any
    environment {
	DOCKERHUB_CREDENTIALS=credentials('dockerid')
	}
     stages{
	   stage('Checkout')  {
	     steps{
		    git branch: 'master', url:'https://github.com/palwalun/java-mvn-springbootapp' 
			} 
		}	
        stage('Build')  {
		steps{
		   echo "Building the job..."
		   sh "mvn clean package"
		   }
		  }
        stage('Docker Image & Deploy')  {
		steps{
		sh """
		
		  docker build -t palwalun/java-mvn-springbootapp:v1.1 . 
		  docker tag palwalun/java-mvn-springbootapp:v1.1 palwalun/springbootapp:latest
		
		"""
		}
	}
      stage('Run_Container') {
	  steps{
	     sh "docker run -it -p 8086:8080 --name springbootapp palwalun/springbootapp:latest"
		 }
	   }	
	 stage('Login2Dockerhub')  {
	 steps{
	  sh 'echo $DOCKERHUB_CREDENTIAL_PSW | docker login -u $DOCKERHUB_CREDENTIAL_USR --password-stdin
	  }
	 }
	 stage('Publish-to-docker-registry'){
	 steps{
	    sh 'docker push palwalun/springbootapp:latest'
		}
	}
  }
}