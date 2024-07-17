pipeline {
    agent any
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials-id')  // Jenkins credentials ID for Docker Hub
    }

    stages {
        stage('Pull Code') {
            steps {
                // Step 1: Pull code from GitHub
                git branch: 'main', credentialsId: 'github-credentials-id', url: 'https://github.com/fahmydiab/simple-nodejs-practice-docker-fork.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Step 2: Build Docker image
                script {
                    def customImage = docker.build("fahmy1diab/ci_cd_practice:v1", ".")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Step 3: Push Docker image to Docker Hub
                script {
                    docker.withRegistry('', 'docker-hub-credentials-id') {
                        docker.image("fahmy1diab/ci_cd_practice:v1").push()
                    }
                }
            }
        }

        stage('Deploy Docker Image') {
            steps {
                // Step 4: Deploy Docker image (replace with your deployment commands)
                sh "docker run -d -p 3000:3000 ${DOCKER_HUB_CREDENTIALS_USR}/ci_cd_practice:v1"
            }
        }
    }
}
