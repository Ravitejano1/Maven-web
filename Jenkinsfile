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
				file: 'Maven-web/target/SRE.war', 
				type: 'war'
				]
			],
				credentialsId: 'nexus3',
				groupId: 'Sidgs-SRE', 
				nexusUrl: '35.171.189.204:8081/#browse/browse:Sidgs-Release-repository', 
				nexusVersion: 'nexus3', 
				protocol: 'http', 
				repository: 'Sidgs-Release-repository', 
				version: '2.0.0-SNAPSHOT'
			}
	}
   
	
