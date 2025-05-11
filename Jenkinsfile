pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flipkart-clone-local'
        CONTAINER_NAME = 'flipkart-clone-container'
    }

    stages {
        stage('Clone Repo') {
            steps {
                // Make sure to specify the branch (e.g., main)
                git branch: 'main', url: 'https://github.com/shreeshailk09/flipcart-clone.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the docker image using the environment variable
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                // Stop and remove the existing container if it exists
                sh """
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                """
            }
        }

        stage('Run New Container') {
            steps {
                // Run a new container from the built image
                sh 'docker run -d -p 80:80 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}
