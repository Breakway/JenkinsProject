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
                        docker.image('my-app:latest').inside {
                        sh 'python3 hello.py'
                        }
                }
            }
        }
    }
    post {
        always{
            emailext{
                subject: "Результат сборки",
                body: "Сборка завершена. Docker-образ готов.",
                to: 'dechikarenkov@gmail.com'    
            }
        }
    }

    
}
