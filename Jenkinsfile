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
        stage('Push Docker Image') {
            steps {
                script {
                     docker.withRegistry('https://registry.hub.docker.com', 'docker-credentials') {
                          sh 'docker push IBreakway/my-app:latest'
                }
            }
        }
    }
    post {
        always{
            emailext(
                to: 'dechikarenkov@gmail.com',  
                subject: 'Результат сборки',
                body: 'Сборка завершена. Docker-образ готов.'   
            )
        }
    }

    }
}
