pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nextjs-app"
        IMAGE_NAME = "nesths-image"
        EMAIL = "zeeshan40132@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo'){
            steps{
                git branch: 'main', url: 'https://github.com/zeeshan40132/CI-CD-Pipeline-using-jenkins-github-webhook-ubuntu-docker-amazon-ec2.git'
            }
        }
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Stop and Remove Previous Container'){
            steps{
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }
        stage('Docker Container Run'){
            steps{
                sh '''
                    docker run -d -p ${port}:${port} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        stage('send email notification'){
            steps{
                emailext(
                    subject: "NextJS App Deployed successfully on EC2",
                    body: "Your nextjs app is deployed at http://13.53.110.19:3000/",
                    to: "${EMAIL}"
                )
            }
        }

    }
}

