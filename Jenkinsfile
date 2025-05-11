pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flipkart-clone-local'
        CONTAINER_NAME = 'flipkart-clone-container'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/shreeshailk09/flipcart-clone.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                sh """
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                """
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}
