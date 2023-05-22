pipeline{
    agent any
    stages {
        stage('Clone') {
            git 'https://github.com/datnguyen1909/Jenkins-pipeline-test.git'
        }
        stage('Build') {
            echo 'build application'
        }
        stage('Test') {
            echo 'test application'
        }
        stage ('Deploy') {
            echo 'Deploy application'
        }
    }
}