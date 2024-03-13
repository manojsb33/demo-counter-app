pipeline {
    agent any
    stages{
        stage('Git check out') {
            steps{
                git branch: 'main', url: 'https://github.com/manojsb33/demo-counter-app.git'
            }
        }
    }
}
