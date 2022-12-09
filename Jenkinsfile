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
       	sh "${mavenCMD} admin:admin123"    	
    }
}
     stage('upload war to nexus'){
	        steps{
	            nexusArtifactUploader artifacts: [
	          
	                artifactId: 'SRE', 
	                classifier: '', 
	                file: 'target/SRE-1.5.war', 
	                type: 'war'
	                ]           
	                credentialsId: 'admin', 
	                groupId: 'Sidgs-SRE', 
	                nexusUrl: '54.243.2.154:8081', 
	                nexusVersion: 'nexus3', 
	                protocol: 'http', 
	                repository: 'Sidgs-Releases', 
	                version: '1.5'
		}
	}
}
