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
                sh 'npm run lint'
            }
        }
        stage ('Deploy') {
            steps{
                echo 'Deploy application'
                sh 'git config --global user.email "datns1610@gmail.com"'
                sh 'git config --global user.name "Nguyen Duy Dat"'
                sh 'npm run deploy'
            }
        }
    }
    post {
        always {
            emailext body: 'A Test EMail', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
            subject: 'Test',
            to: 'datns1610@gmail.com'
        }
    }
}