node{
    
    stage('Checkout code'){
       checkout scm
    }
    
    stage ('Compile'){
        withMaven(jdk: 'jdk11', maven: 'maven3'){
        sh 'mvn compile'
        }
    }
    
    stage ('Unit Testing'){
        withMaven(jdk: 'jdk11', maven: 'maven3'){
        sh 'mvn test'
        }
    }
    stage ('Package'){
        withMaven(jdk: 'jdk11', maven: 'maven3'){
        sh 'mvn package'
        }
    }
    
    stage ('Publish Test Report'){
        junit 'target/**/*.xml'
    }
    
    stage ('Archive Artifact'){
        archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false    
    }
    
    stage('Email Notification'){
        emailext attachLog: true, body: '', subject: 'Build Successful', to: 'luke.marshall.03@gmail.com'
    }
    
    stage('Slack Notify'){
        slackSend channel: 'jenkins-slack-test', message: 'This is a slack test message.'
    }
    
}