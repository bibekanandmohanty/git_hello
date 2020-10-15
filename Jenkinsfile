pipeline {
    agent any
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
	         script {
	         def mavenPom = readMavenPom file: 'pom.xml'
                 nexusArtifactUploader artifacts: [
		              [
			         artifactId: 'simple-app',
				 classifier: '',
				 file: "target/simple-app-${mavenPom.version}.war',
				 type: 'war'
			     ]
	         ], 
		 credentialsId: 'nexus',
		 groupId: 'in.javahome', 
		 nexusUrl: '157.245.138.63:8081', 
		 nexusVersion: 'nexus3', 
		 protocol: 'http', 
		 repository: 'CI-SimpleApp',
		 version: '${mavenPom.version}'
                } 
	    }
        }
    }
}    
