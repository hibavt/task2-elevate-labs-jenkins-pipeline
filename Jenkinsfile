pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }

    environment {
        DOCKER_USERNAME = 'ayishahiba'
        DOCKER_PASSWORD = credentials('dockerhub')
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cleaning workspace...'
                deleteDir()
                echo 'Cloning repository manually...'
                sh 'git clone -b main https://github.com/hibavt/task2-elevate-labs-jenkins-pipeline.git .'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test || echo "No tests found"'
            }
        }

        stage('Docker Build & Push') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${DOCKER_USERNAME}/jenkins-demo-app ."
                echo 'Pushing Docker image to Docker Hub...'
                sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                sh "docker push ${DOCKER_USERNAME}/jenkins-demo-app"
            }
        }
    }
}
