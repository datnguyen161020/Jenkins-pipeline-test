pipeline{
    agent any
    tools { nodejs "nodejs" }
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
                sh 'git init'
                sh 'git branch gh-pages'
                sh 'npm run deploy'
            }
        }
    }
}