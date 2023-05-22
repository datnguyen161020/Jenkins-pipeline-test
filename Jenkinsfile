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
                sh 'git config --global user.email "datns1610@gmail.com"'
                sh 'git config --global user.name "Nguyen Duy Dat"'
                sh 'git init'
                sh 'npm run deploy'
            }
        }
    }
}