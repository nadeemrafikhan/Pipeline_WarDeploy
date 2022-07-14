pipeline {
			agent any 
				stages {
					stage ('git checkout') {
					   steps { 
					   		git credentialsId: 'github', url:'https://github.com/nadeemrafikhan/hello-world.git'
					   		}
					   		}
					stage ('Build') {
						steps {					
							sh '/opt/apache-maven-3.8.6/bin/mvn clean package'
}
}
				}
}
