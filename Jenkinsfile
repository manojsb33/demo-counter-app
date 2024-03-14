pipeline {
    agent any
    stages{
        stage('Git check out') {
            steps{
                git branch: 'main', url: 'https://github.com/manojsb33/demo-counter-app.git'
            }
        }
        stage('Unit test maven') {
            steps{
                sh 'mvn test'
            }
        }
        stage('maven integration test') {
            steps{
                sh 'mvn verify'
            }
        }
        stage('Maven build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Coad Quality analysis') {
            steps {
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-hi') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage('Quality Gate Status'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-hi'
                }
            }
        }
        stage('upload war file to nexus') {
            steps{
                script{
                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'springboot', 
                            classifier: '', file: 'target/Uber.jar', 
                            type: 'jar'
                            ]
                    ], 
                    credentialsId: 'sonar-nexus', 
                    groupId: 'com.example', 
                    nexusUrl: '54.234.80.194:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'demo-app-release', version: '1.0.0'
                }
            }
        }
    } 
}
