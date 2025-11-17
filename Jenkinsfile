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
		
		  docker build -t palwalun/springbootapp:latest .
		
		"""
		}
	}
      stage('Run_Container') {
	  steps{
	     sh "docker run -d -p 8086:8080 --name springbootapp palwalun/springbootapp:latest"
		 }
	   }	
	 
  }
}