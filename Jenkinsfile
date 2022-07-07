pipeline {
		agent any 
		   stages {
		            stage ('Build'){
						steps {					
						 	//sh script: 'mvn clean package'
							sh '/opt/apache-maven-3.8.6/bin/mvn clean package'
							//archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
						}
				    post {
  always {
    cleanWs()
    dir("${env.WORKSPACE}@tmp") {
      deleteDir()
    }
    dir("${env.WORKSPACE}@script") {
      deleteDir()
    }
    dir("${env.WORKSPACE}@script@tmp") {
      deleteDir()
    }
  }
}
                  }
                }
}
