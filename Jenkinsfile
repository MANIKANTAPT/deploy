pipeline {
    agent any

    tools {
        maven 'local_maven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to Server') {
            steps {
                script {
                    def credentialsId = '7e29506f-5ca2-4334-b373-390a3ec4f734'
                    def tomcatUrl = 'http://3.109.139.88:8000/'

                    deploy adapters: [tomcat9(credentialsId: credentialsId, path: '', url: tomcatUrl)],
                           contextPath: null,
                           war: '**/*.war'
                }
            }
        }
    }
}
