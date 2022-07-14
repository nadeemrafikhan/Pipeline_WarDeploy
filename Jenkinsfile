pipeline {
	agent any 
	options {
	        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
	    }
           //variable declaration 
		 environment {
				PATH= "/opt/apache-maven-3.8.6/bin/:$PATH"
				def WAR_PATH= "webapp/target/*.war"
		} 
	stages {
	
// In this checkout stage, integrating github repo with Jenkins
stage ('git checkout') {
	           steps { 
	 	git credentialsId: 'github', url:'https://github.com/nadeemrafikhan/hello-world.git'
		}

	}
// In this build stage , cleaning the workspace before package the .war file on local Jenkins server.				   		

	stage ('Build') {
	           steps {	
// before environment variable setup
//sh '/opt/apache-maven-3.8.6/bin/mvn clean package’
//after environment valoiable setup				
	sh 'mvn clean package'
	}
	}
	
// In this deploy stage .war file will be deployed on to the tomcat server, tocat_ssh is the credentials of the ec-user where these credentials added into the Jenkins using .PEM file of the ec2 instance.
//In post section we did archive the succuss plugin into the tomcat server but on different location using same credentials.

stage ('deploy') {
		steps {

		/* 
		using c2-user and its .pem file to uplad .war file
		sshagent(['tocat_ssh']) {
	// Before war file path variable setup
 //sh 'scp -o StrictHostkeyChecking=no   webapp/target/*.war  ec2-user@43.204.24.96:/opt/apache-tomcat-8.5.81/webapps/'

//after war file path variable setup
sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} ec2-user@43.204.24.96:/opt/apache-tomcat-8.5.81/webapps/'
	}
	} 
			post{
	                success{
	                    echo 'Now Archiving ....'
			    archiveArtifacts artifacts : '**\/*.war' 
	                    sshagent(['tocat_ssh']) {
	                    sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} ec2-user@43.204.24.96:/home/ec2-user/artifact/'
	                }
			}
	            }
*/

		// using root and its prite key file to uplad .war file
		sshagent(['root-ssh']) {
	// Before war file path variable setup
 //sh 'scp -o StrictHostkeyChecking=no   webapp/target/*.war  root@43.204.24.96:/opt/apache-tomcat-8.5.81/webapps/'
//after war file path variable setup
sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} root@43.204.24.96:/opt/apache-tomcat-8.5.81/webapps/'
	}
	} 
			post{
	                success{
	                    echo 'Now Archiving ....'
			    archiveArtifacts artifacts : '**/*.war' 
	                    sshagent(['root-ssh']) {
	                    sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} root@43.204.24.96:/home/ec2-user/artifact/'
	                }
			}
	            }

		
		}	
				
					}
	}
