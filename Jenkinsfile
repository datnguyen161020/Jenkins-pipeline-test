pipeline{
    agent any
    stages {
        stage('Build') {
            steps{
                echo 'build application'
                sh 'npm install'
                sh 'npx next build'
            }
        }
        stage('Test') {
            steps{
                echo 'test application'
            }
        }
        stage ('Deploy') {
            steps{
                echo 'Deploy application'
                sh 'npm run deploy'
            }
        }
    }
}