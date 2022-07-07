pipeline {
		agent any 
		   stages {
		            stage ('Build'){
						steps {					
						 	sh '/opt/apache-maven-3.8.6/bin/mvn clean package'
							//archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
						}
                  }
                }
}
