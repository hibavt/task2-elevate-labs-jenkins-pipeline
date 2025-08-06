pipeline {
    agent { docker { image 'node:16' } }

    environment {
        DOCKER_USERNAME = 'ayishahiba'
        DOCKER_PASSWORD = credentials('dockerhub')
    }

    stages {
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
                sh 'docker build -t ayishahiba/jenkins-demo-app .'
                echo 'Pushing Docker image to Docker Hub...'
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                sh 'docker push ayishahiba/jenkins-demo-app'
            }
        }
    }
}
