pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t portfolio-website:v2 .'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat '''
                docker rm -f portfolio-container || exit 0
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker run -d --name portfolio-container -p 8080:80 portfolio-website:v2
                '''
            }
        }
    }

    post {
        success {
            echo 'Build Successful!'
        }

        failure {
            echo 'Build Failed!'
        }
    }
}