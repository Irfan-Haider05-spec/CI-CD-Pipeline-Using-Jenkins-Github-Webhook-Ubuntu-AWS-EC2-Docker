pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "irfanbangash14125@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('CLone Repo') {
            steps {
                git branch: 'main', url:'https://github.com/Irfan-Haider05-spec/CI-CD-Pipeline-Using-Jenkins-Github-Webhook-Ubuntu-AWS-EC2-Docker.git';
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove Previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME ||true
                '''
            }
        }

        stage('Docker Container Run') {
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        stage('Send Email Notification') {
            steps {
                emailext(
                    subject: 'NestJS App Deployed Successfully!',
                    body: 'Your NestJS App is Deployed Successfully! http://13.60.57.122:${PORT}/',
                    to: "${EMAIL}"
                )
            }
        }
    }
}