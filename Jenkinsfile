node{
    
   		 stage('Clone repo'){
       		 git branch: 'main', credentialsId: 'Githubcredentials', url: 'https://github.com/Ravitejano1/Maven-web.git'
    		}
    
    		stage('Maven Build'){
        	def mavenHome = tool name: "Maven-3.8.6", type: "maven"
        	def mavenCMD = "${mavenHome}/bin/mvn"
        	sh "${mavenCMD} clean package"
    		}
    
     		stage('SonarQube analysis') {       
        	withSonarQubeEnv('Sonar-Server-7.8') {
		def mavenHome = tool name: "Maven-3.8.6", type: "maven"
        	def mavenCMD = "${mavenHome}/bin/mvn"
       		sh "${mavenCMD} sonar:sonar"    	
    		}
	}
	
		stage('upload war to nexus'){
			nexusArtifactUploader artifacts: [
			[
				artifactId: 'SRE', 
				classifier: '', 
				file: 'target/SRE.war', 
				type: 'war'
				]
			],
				credentialsId: 'nexus3',
				groupId: 'Sidgs-SRE', 
				nexusUrl: 'http://3.94.252.186:8081/repository/Sidgsrelease/', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'Sidgsrelease', 
				version: '1.0.0'
			}
	}
   
	
