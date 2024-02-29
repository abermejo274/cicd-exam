pipeline {
    agent any
    
    environment {     
        DOCKER_TOKEN = credentials('docker-token')     
    } 

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abermejo274/cicd.git'
            }
        }
        stage('Docker Build') {
            steps {
                 sh 'docker build -t abermejo274/ci-exam-docker-image:${BUILD_NUMBER} .'
                }
            }
        stage('Docker Login & Push') {
            steps {
                    sh('docker login -u abermejo274 -p $DOCKER_TOKEN')
                    sh 'docker push abermejo274/ci-exam-docker-image:${BUILD_NUMBER}'
                }
            }
        stage('Deploy App via Helm') {
            steps {
                sh 'helm uninstall nginx-app'
                //  sh 'helm install nginx-app cicd'
                sh 'helm upgrade --install nginx-app cicd'
                 
                }
            }
    }
}