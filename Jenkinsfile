pipeline{
    agent any
    tools{
        maven 'local_maven'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts : '**/target/*.war'
                }
            }
        }
        stage('Deploy to Server'){
            steps{
               deploy adapters: [tomcat9(credentialsId: '7e29506f-5ca2-4334-b373-390a3ec4f734', path: '', url: 'http://3.109.139.88:8080/')], contextPath: null, war: '**/*.war'
        }
    }
}
