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
    } 
}
