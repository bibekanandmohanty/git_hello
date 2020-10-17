pipeline {
    agent any
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh 'mvn clean package'
            }
        }
        stage('Upload War To Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [
		              [
			         artifactId: 'simple-app',
				 classifier: '',
				 file: "target/simple-app-1.0.0.war",
				 type: 'war'
			     ]
	         ], 
		 credentialsId: 'nexus',
		 groupId: 'in.javahome', 
		 nexusUrl: '165.227.83.122:8000', 
		 nexusVersion: 'nexus3', 
		 protocol: 'http', 
		 repository: 'CI',
		 version: '1.0.0'
                 
	    }
        }
    }
}    
