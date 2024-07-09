//Diplay build version with your jon name display

//currentBuild.displayName="${latestTag}~#"+currentBuild.number
currentBuild.displayName="war_deploy~#"+currentBuild.number
pipeline {
    agent any 
    options {
        //Days to keep builds is 5 and Max # of builds to keep is 7
            buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
        }
           //variable declaration 
         environment {
                PATH= "/opt/apache-maven-3.8.6/bin/:$PATH"
                def WAR_PATH= "webapp/target/*.war"
             //latestTag = sh(returnStdout:  true, script: "git tag --sort=-creatordate | head -n 1").trim()
             //latestTag = 'ddddddddddddddddd'
        } 
    stages {
    
/* In this checkout stage, integrating github repo with Jenkins but this stage will only use if your pipeline jos definition is pipeline script
this you will select when you create job and in pipeline section and there you have to paste these content there, 
so In this example I am using different method that pipeline script from SCM
stage ('git checkout') {
               steps { 
        //git credentialsId: 'github', url:'https://github.com/nadeemrafikhan/hello-world.git'
        git 'https://github.com/nadeemrafikhan/hello-world.git'
        }

    }
    */
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

        
        //using c2-user and its .pem file to uplad .war file
        sshagent(['tocat_ssh']) {
    // Before war file path variable setup
 //sh 'scp -o StrictHostkeyChecking=no   webapp/target/*.war  ec2-user@43.204.24.96:/opt/apache-tomcat-8.5.81/webapps/'

//after war file path variable setup
sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} ec2-user@13.233.140.147:/opt/apache-tomcat-8.5.81/webapps/'
    }
    } 
            post{
                    success{
                        echo 'Now Archiving ....'
                archiveArtifacts artifacts : '**/*.war' 
                        sshagent(['tocat_ssh']) {
                        sh """
                        scp -o StrictHostkeyChecking=no ${WAR_PATH} ec2-user@13.233.140.147:/home/ec2-user/artifact/
                        ssh ec2-user@13.233.140.147 /opt/apache-tomcat-8.5.81/bin/shutdown.sh
                        ssh ec2-user@13.233.140.147 /opt/apache-tomcat-8.5.81/bin/startup.sh
                        """
                    }
            }
                }

/*
        // using root and its prite key file to uplad .war file
        sshagent(['root-ssh']) {
    // Before war file path variable setup
 //sh 'scp -o StrictHostkeyChecking=no   webapp/target/*.war  root@13.235.23.39:/opt/apache-tomcat-8.5.81/webapps/'
//after war file path variable setup
sh """
    scp -o StrictHostkeyChecking=no ${WAR_PATH} root@13.235.23.39:/opt/apache-tomcat-8.5.81/webapps/
    ssh root@13.235.23.39 /opt/apache-tomcat-8.5.81/bin/shutdown.sh
    ssh root@13.235.23.39 /opt/apache-tomcat-8.5.81/bin/startup.sh
""" 
} 
    } 
            post{
                    success{
                        echo 'Now Archiving ....'
                archiveArtifacts artifacts : '**\/*.war' 
                        sshagent(['root-ssh']) {
                        sh 'scp -o StrictHostkeyChecking=no ${WAR_PATH} root@13.235.23.39:/home/ec2-user/artifact/'
                    }
            }
                }
*/
        
        }   
                
                    }
    }














################################################
To create a new Jenkins pipeline and transfer an old pipeline configuration to a new environment, you can follow these steps:
 
### 1. **Create a New Jenkins Pipeline**
 
#### Step 1: Access Jenkins Dashboard
1. Open Jenkins in your web browser.
2. Log in with your credentials.
 
#### Step 2: Create a New Pipeline
1. Click on "New Item" on the Jenkins dashboard.
2. Enter a name for your new pipeline.
3. Select "Pipeline" as the project type.
4. Click "OK".
 
#### Step 3: Configure Pipeline
1. In the pipeline configuration page, you can define your pipeline script. You can use either the Jenkins Pipeline DSL (Declarative or Scripted).
2. Here is an example of a simple declarative pipeline script:
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    echo 'Building...'
                }
            }
            stage('Test') {
                steps {
                    echo 'Testing...'
                }
            }
            stage('Deploy') {
                steps {
                    echo 'Deploying...'
                }
            }
        }
    }
    ```
 
3. Save the pipeline configuration.
 
### 2. **Transfer Old Jenkins Pipeline Configuration to New Environment**
 
#### Step 1: Export Old Pipeline Configuration
1. Go to the old pipeline configuration page.
2. Copy the pipeline script from the "Pipeline" section.
 
#### Step 2: Import Configuration to New Pipeline
1. Open the new pipeline configuration page.
2. Paste the copied pipeline script into the "Pipeline" section.
3. Save the new pipeline configuration.
 
### 3. **Transfer Environment Variables and Credentials**
 
#### Step 1: Transfer Environment Variables
1. If your old pipeline uses environment variables, transfer them to the new environment.
2. In the pipeline configuration page, you can set environment variables in the "Environment Variables" section or directly in the pipeline script:
    ```groovy
    environment {
        MY_VAR = 'my_value'
    }
    ```
 
#### Step 2: Transfer Credentials
1. Go to the Jenkins "Manage Jenkins" > "Manage Credentials" section.
2. Export the necessary credentials from the old environment.
3. Import the credentials to the new environment under the appropriate domain.
 
### 4. **Testing the New Pipeline**
1. Run the new pipeline by clicking "Build Now".
2. Monitor the pipeline execution and ensure all steps are executed correctly.
 
### Additional Tips:
- If your old pipeline uses shared libraries, ensure they are accessible in the new environment.
- Adjust any environment-specific paths or configurations in the pipeline script.
- Verify plugin compatibility if your old pipeline relies on specific Jenkins plugins.
 
By following these steps, you should be able to successfully create a new Jenkins pipeline and transfer the old pipeline configuration to a new environment.
###############################################
