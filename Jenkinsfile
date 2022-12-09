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
	 	            nexusArtifactUploader artifacts: 
			    [
				    [
					    artifactId: 'SRE', 
					    classifier: '', 
					    file: 'target/SRE.war', 
					    type: 'war'
				    ]
			    ], 
			    credentialsId: 'Nexuscredentials', 
			    groupId: 'Sidgs-SRE', 
			    nexusUrl: '10.7.1.39', 
			    nexusVersion: 'nexus3', 
			    protocol: 'http', 
			    repository: 'http://54.224.241.114:8081/repository/Sidgs-SRE-Releases/', 
			    version: '1.0.0'
		}
	}

