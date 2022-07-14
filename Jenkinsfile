 pipeline {
			agent any 
	options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
	environment {
			PATH= "/opt/apache-maven-3.8.6/bin/:$PATH"
			def WAR_PATH= "webapp/target/*.war"
	}
				stages {
					stage ('git checkout') {
					   steps { 
					   		git credentialsId: 'github', url:'https://github.com/nadeemrafikhan/hello-world.git'
					   		}
					   		}
					stage ('Build') {
						steps {					
							sh 'mvn clean package'
}
}
					stage ('deploy') {
	steps {
	sshagent(['tocat_ssh']) {
		sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} ec2-user@43.204.24.96:/opt/apache-tomcat-8.5.81/webapps/'
}
}
		post{
                success{
                    echo 'Now Archiving ....'
		    archiveArtifacts artifacts : '**/*.war' 
                     sshagent(['tocat_ssh']) {
                    sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} ec2-user@43.204.24.96:/home/ec2-user/artifact/'
                }
		}
            }
}	
			
				}
}
