pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }

    stages {

        stage ('Git Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/gopi732/spring-pet.git']]])
            }
        }
        
        stage ('Build Docker Image') {
            steps {
                sh 'docker-compose build '       
            }
        }
        stage ('Rename Docker Image') {
            steps {
                sh 'docker tag spring-pet_database  saigopi123456/spring-database'
                sh 'docker tag spring-pet_spring saigopi123456/spring-app'       
            }
        }
        stage ('Login DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR  --password-stdin'       
            }
        }
        stage ('push Docker images') {
            steps {
                sh 'docker push saigopi123456/spring-database'
                sh 'docker push saigopi123456/spring-app'

            }
        }
        stage ('Remove Docker Images') {
            steps {
                sh 'docker rmi -f $(docker images -a -q)'
            }
        }
    }
}
