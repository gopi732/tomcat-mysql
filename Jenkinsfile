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
        stage ('Clean up') {
            steps {
                sh 'docker stop $(docker ps -a -q) || true && docker rm $(docker ps -a -q) || true && docker rmi -f $(docker images -a -q) || true'  
            }
        }
        stage ('Build Docker Image') {
            steps {
                sh 'docker-compose build '       
            }
        }
        stage ('Rename Docker Image') {
            steps {
                sh 'docker tag tomcat-mysql_mydb  saigopi123456/tomcat-db'
                sh 'docker tag tomcat-mysql_web saigopi123456/tomcat-web'       
            }
        }
        stage ('Login DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR  --password-stdin'       
            }
        }
        stage ('push Docker images') {
            steps {
                sh 'docker push saigopi123456/tomcat-db'
                sh 'docker push saigopi123456/tomcat-web'

            }
        }
    }
}
