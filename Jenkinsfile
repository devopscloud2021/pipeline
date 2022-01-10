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
                            file: "target/wwp-2.0.0.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus', 
                    groupId: 'koddas.web.war', 
                    nexusUrl: '13.251.156.112:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'test-release', 
                    version: '2.0.0'
                    }
            }
        }
  }
