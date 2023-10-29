pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Test') {
            steps {
                dir('sources') {
                sh 'python hello.py'
                }
            }
        }
    }
}
