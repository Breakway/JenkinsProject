pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                    sh 'docker build - t ibreakway/jenkins_project:latest'
            }
        }
        Stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {       
                  sh 'docker push ibreakway/jenkins_project:latest'
                }
            }
        }
    post {
        always{
           sh 'docker logout'
        }
    }
}
