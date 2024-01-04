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
        stage('Creating Artifact'){
            steps{
                archiveArtifacts artifacts: 'build/**/*', followSymlinks: false
            }
        }
        stage ('Deploy') {
            steps{
                echo 'Deploy application'
                sh 'npx next build'
                sshPublisher(publishers: [sshPublisherDesc(configName: 'window', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'build', remoteDirectorySDF: false, removePrefix: '/build', sourceFiles: '/build/**/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'window', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'C:\\Windows\\System32\\xcopy.exe /e /K /D /H /Y C:\\Users\\Admin\\deploy\\build "F:\\test"', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])             
                // sshPublisher(publishers: [sshPublisherDesc(configName: 'window', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'C:\\Windows\\System32\\cmd.exe /s /c rmdir /s /q C:\\Users\\Admin\\deploy\\build', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])             
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