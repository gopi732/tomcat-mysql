pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        http_proxy = 'http://127.0.0.1:3128/'
        https_proxy = 'http://127.0.0.1:3128/'
        ftp_proxy = 'http://127.0.0.1:3128/'
        socks_proxy = 'socks://127.0.0.1:3128/'
    }

    stages {
        
        stage ('Build Docker Image') {
            steps {
                sh 'docker-compose build '       
            }
        }
        stage ('Login DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR  --password-stdin'       
            }
        }
        stage ('push Docker images') {
            steps {
                sh 'docker push saigopi123456/tomcat-mysql_mydb:latest'
                sh 'docker push saigopi123456/tomcat-mysql_web:latest'

            }
        }
        stage ('Remove Docker Images') {
            steps {
                sh 'docker rmi -f $(docker images -a -q)'
            }
        }
    }
}
