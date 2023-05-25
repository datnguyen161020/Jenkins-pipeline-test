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
            echo 'This will always run'  
        }  
        success {  
        emailext body: 'Build SUCCESS', 
        recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
        subject: 'Test pipeline',
        to: 'datns1610@gmail.com'  
        }  
        failure { 
        emailext body: 'Build Fail', 
        recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], 
        subject: 'Test',
        to: 'datns1610@gmail.com' 
        }  
        unstable {  
        echo 'This will run only if the run was marked as unstable'  
        }  
        changed {  
        echo 'This will run only if the state of the Pipeline has changed'  
        echo 'For example, if the Pipeline was previously failing but is now successful'  
        }
    }
}