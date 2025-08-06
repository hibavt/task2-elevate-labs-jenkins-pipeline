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
                git branch: 'main', url: 'https://github.com/hibavt/task2-elevate-labs-jenkins-pipeline.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm install'
            }
        }
