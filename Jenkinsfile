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
}
   
	
