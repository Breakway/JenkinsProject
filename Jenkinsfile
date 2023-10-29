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
        stage ('Tag Docker Image') {
            steps {
                script {
                    sh 'docker tag my-app:latest ibreakway/jenkins_project'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                        withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                        sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'
                    }
                    
                    sh 'docker push ibreakway/jenkins_project/my-app:latest'
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
