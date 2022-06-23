// Declarative pipeline
pipeline {
    agent any

    stages {

        stage ('Git Checkout') {
            steps {
                git branch: 'master', credentialsId: 'github', url: 'https://github.com/gopi732/tomcat-mysql.git'
            }
        }
        
        stage ('Build Docker Image') {
            steps {
                sh 'docker-compose build '       
            }
        }
    }
}
