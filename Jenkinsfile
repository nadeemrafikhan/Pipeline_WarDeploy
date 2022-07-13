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
			sh 'scp -o StrictHostkeyChecking=no target/*.war root@172.31.38.66:/opt/apache-tomcat-8.5.81/webapps/'
						}
						}
						}
						}
