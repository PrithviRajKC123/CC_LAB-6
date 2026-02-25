pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                script {
                    docker.build("lab6-backend", "./backend")
                }
            }
        }

        stage('Run Backend Container') {
            steps {
                script {
                    docker.image("lab6-backend").run("-d --name backend-container")
                }
            }
        }

        stage('Deploy NGINX') {
            steps {
                script {
                    docker.image("nginx").run("-d -p 8082:80 --name nginx-container")
                }
            }
        }
    }
}
