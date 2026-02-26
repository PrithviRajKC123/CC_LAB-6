pipeline {
    agent any

    stages {

        stage('Create Network') {
            steps {
                sh '''
                docker network create lab-network || true
                '''
            }
        }

        stage('Build Backend Image') {
            steps {
                sh '''
                docker build -t backend-app backend
                '''
            }
        }

        stage('Run Backend Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true
                docker run -d --name backend1 --network lab-network backend-app
                docker run -d --name backend2 --network lab-network backend-app
                '''
            }
        }

        stage('Deploy NGINX') {
            steps {
                sh '''
                docker rm -f nginx-lb || true
                docker run -d --name nginx-lb -p 80:80 --network lab-network nginx
                sleep 2
                docker cp nginx/default.conf nginx-lb:/etc/nginx/conf.d/default.conf
                docker exec nginx-lb nginx -s reload
                '''
            }
        }
    }
}
