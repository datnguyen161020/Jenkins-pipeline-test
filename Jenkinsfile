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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'window', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'scp admin@192.168.0.102 package.json', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'package.json')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])            
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