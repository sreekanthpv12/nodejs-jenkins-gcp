pipeline {
    agent any

    environment {
        build_number = "${env.BUILD_ID}"
        //DOCKERHUB_CREDENTIALS = 'dockerhub'
        DOCKERHUB_CREDENTIALS = credentials('sree-dockerhub')
    }
    
    tools {
        maven 'maven'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sreekanthpv12/nodejs-jenkins-gcp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t sreekanthpv12/nodejs-app-demo:latest .'
                }
            }
        }
           stage('login to dockerhub & deploy image') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push sreekanthpv12/nodejs-app-demo:latest'
            }
        }
        // stage('remove image from local') {
        //     steps{
        //         sh 'docker rmi -f sreekanthpv12/nodejs-app-demo:latest'
                
        //     }
        // }
        // stage('pull image from dockerhub') {
        //     steps{
        //         sh ' docker pull sreekanthpv12/nodejs-app-demo:latest'
        //     }
        // }
        stage('docker-compose to deploy ') {
            steps {
                sh 'docker-compose down -v'
                sh 'docker-compose up -d'
            }
        }
        
        
   }

}
