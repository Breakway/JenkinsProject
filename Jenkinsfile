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
                script {
                    docker.build('my-app:latest')
                }

                script {
                    dcoker.image('my-app:latest').inside {
                    sh 'python3 hello.py'
                    }
            }
        }
    }
}
}
