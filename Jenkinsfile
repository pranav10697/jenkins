pipeline {
    agent any
    stages {
        stage('Pull') {
            steps {
                git 'https://github.com/pranav10697/studentapp-ui.git'
            }
        }
        stage('Build') {
            steps { 
                 sh 'mvn clean package '
            }
        }
        stage('Test') {
            steps {
                withSonarQubeEnv(installationName: 'sonar', credentialsId: 'sonar-creds') {
                sh 'mvn sonar:sonar'
                }
            }
        } 
                stage('Deploy') {
            steps {
                echo '"Deploy successfully"'
            }
        }
    }
} 
