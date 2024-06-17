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
                 sh '/opt/maven/bin/mvn clean package '
            }
        }
        stage('Test') {
            steps {
                withSonarQubeEnv(installationName: 'sonar', credentialsId: 'sonar-creds') {
                sh '/opt/maven/bin/mvn sonar:sonar'
                }
            }
        } 
                stage("Quality Gate"){
                    steps{
                        waitForQualityGate abortPipeline: true
                    }
                }
                stage('Deploy') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat-creds', path: '', url: 'http://100.25.171.136:8080/')], contextPath: '/', war: '**/*.war'
            }
        }
    }
} 
