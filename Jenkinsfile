pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "saigopi123456/tomcat-web"
        DOCKER_HUB_REPOO = "saigopi123456/tomcat-db"
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
                sh 'docker tag tomcat-mysql_mydb $DOCKER_HUB_REPOO && docker tag tomcat-mysql_web $DOCKER_HUB_REPO'      
            }
        }
        stage ('create container'){
            steps {
                    sh 'docker-compose up -d && docker ps'
            }
        }
        stage ('Container Testing '){
            steps {
                    sh 'wget localhost:8088/gameoflife'
            }
        }
        stage ('Login DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR  --password-stdin'       
            }
        }
        stage ('Docker push') {
            steps {
                sh 'docker push $DOCKER_HUB_REPO && docker push $DOCKER_HUB_REPOO'
            }
        }
    }
}
