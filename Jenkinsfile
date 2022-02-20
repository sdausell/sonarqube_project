node {
   def sonarUrl = 'sonar.host.url=http://164.92.245.66:9000'
   def mvn = tool (name: 'maven3', type: 'maven') + '/bin/mvn'
   stage('SCM Checkout'){
    // Clone repo
	git branch: 'master', 
	credentialsId: 'github', 
	url: 'https://github.com/sdausell/demo'
   
   }
   
   stage('Sonar Publish'){
	   withCredentials([string(credentialsId: 'Sonarqube', variable: 'sda_sq_token1')]) {
        def sonarToken = "sonar.login=${sda_sq_token1}"
        sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	 }
      
   }
   
	
   stage('Mvn Package'){
	   // Build using maven
	   
	   sh "${mvn} clean package deploy"
   }
}
