pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3.6.3"
    }

    stages {
        stage('verify') {
            steps{
                sh 'mvn -v'
            }
        }
        stage('checkout') {
            steps{
                git 'https://github.com/seniquel/spring-framework-petclinic.git'
            }
        }
        stage('compile') {
            steps{
                sh 'mvn clean compile'
            }
        }
        stage('test') {
            steps{
                sh 'mvn test'
            }
            post{
                success {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }
    post {
            success {
                //discordSend description: 'Je mange du caca', footer: '', image: '', link: '', result: '', thumbnail: '', title: 'C\'est moi Jenkins', webhookURL: 'https://discordapp.com/api/webhooks/747819422705778738/dHWPHidlNLpiiKftWU84__Ss2LAkws77Swfdk5OWs22qla3hlI1B4zywW8ROg4nAwjRM'
                slackSend channel: 'jenkins-training', color: 'good', message: 'Léo master success', tokenCredentialId: 'slack-token', teamDomain: 'devinstitut'
            }
            failure {
            slackSend channel: 'jenkins-training', color: 'danger', message: 'Léo master fail', tokenCredentialId: 'slack-token', teamDomain: 'devinstitut'
                    
            }
    }
}

