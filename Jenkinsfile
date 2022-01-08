pipeline {
    agent any
    tools {
        maven 'maven-3.8'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'wwp', 
                            classifier: '', 
                            file: "target/wwp-1.0.0.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus-user-credentials', 
                    groupId: 'koddas.web.war', 
                    nexusUrl: '54.169.88.118:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'test-release', 
                    version: '1.0.0'
                    }
            }
        }
  }
