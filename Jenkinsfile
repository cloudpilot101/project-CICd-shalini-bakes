  pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/cloudpilot101/project-CICd-shalini-bakes.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'wsl docker build -t shalini-bakes:%BUILD_NUMBER% .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                    wsl docker stop shalini-bakes || true
                    wsl docker rm shalini-bakes || true
                    wsl docker run -d --name shalini-bakes -p 8081:80 shalini-bakes:%BUILD_NUMBER%
                '''
            }
        }
    }
}
