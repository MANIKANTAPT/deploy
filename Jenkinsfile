pipeline {
    agent any
    tools {
        maven 'local_maven'
    }
 
    environment {
        TOMCAT_SERVER = '3.109.139.88'
        TOMCAT_PORT = '8000'
        TOMCAT_CREDENTIALS_ID = '7e29506f-5ca2-4334-b373-390a3ec4f734' // Jenkins credentials ID for Tomcat authentication
    }
 
    stages {
        stage('Build') {
            steps {
                script {
                    // Customize Maven goals and options as needed
                    sh "mvn clean package"
                }
            }
        }
 
        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Copy the WAR file to the Tomcat server using SCP or any other method
                    withCredentials([usernamePassword(credentialsId: TOMCAT_CREDENTIALS_ID, passwordVariable: 'TOMCAT_PASSWORD', usernameVariable: 'TOMCAT_USER')]) {
                        // Construct the deployment URL within the withCredentials block
def deployUrl = "http://${TOMCAT_USER}:${TOMCAT_PASSWORD}@${TOMCAT_SERVER}:${TOMCAT_PORT}/manager/text/deploy?path=/sample.war"
 
                        // Log a message indicating a successful connection
                        sh "echo 'Connection successful'"
 
                        // Use curl to deploy the WAR file to Tomcat
                        sh "curl --upload-file target/*.war ${deployUrl}"
                    }
                }
            }
        }
    }
}
