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
                script {
                    docker.build("shalini-bakes:${BUILD_NUMBER}")
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh '''
                        # stop old container if exists
                        docker stop shalini-bakes || true
                        docker rm shalini-bakes || true

                        # run new container
                        docker run -d --name shalini-bakes -p 8081:80 shalini-bakes:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}
