pipeline {
			agent any 
				stages {
					stage ('git checkout')
					   steps { 
					   		git credentialsId: 'github', url:'https://github.com/nadeemrafikhan/hello-world.git'
					   		}
					   		}
					stage ('Build'){
						steps {					
							sh '/opt/apache-maven-3.8.6/bin/mvn clean package'
}
}
	stage ('deploy') {
	steps {
	sshagent(['tocat_ssh']) {
	sh 'scp -o StrictHostkeyChecking=no webapp/target/*.war ec2-user@3.109.60.174:/opt/apache-tomcat-8.5.81/webapps/'
}
}
}
}
}
