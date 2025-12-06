pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = "ashokdocker2405/titan-app"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Clean workspace if needed
                // cleanWs()
                
                git branch: 'main',
                    url: 'https://github.com/TodFrank12/sample-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker Image: ${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}"
                    docker.build("${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    echo "Pushing image to Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("${env.DOCKER_HUB_REPO}:${env.IMAGE_TAG}").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed. Please check logs."
        }
    }
}
