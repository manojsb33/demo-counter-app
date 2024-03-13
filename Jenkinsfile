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
    }
}
