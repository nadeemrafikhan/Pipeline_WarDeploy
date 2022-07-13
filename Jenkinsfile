pipeline {
							agent any 
								stages {
									stage ('Build'){
											steps {					
								sh '/opt/apache-maven-3.8.6/bin/mvn clean package'
                      }
						}
									stage ('deploy') {
											steps {
												sshagent(['tocat_ssh']) {
			sh 'scp -o StrictHostkeyChecking=no **/*.war ec2-user@13.127.165.102:/opt/apache-tomcat-8.5.81/webapps/'
						}
						}
						}
						}
						}
