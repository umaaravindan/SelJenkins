pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('your-credentials-id')
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh '''
                    docker build -t chatlearning123/getting-started:latest .
                    '''
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh '''
                    echo $DOCKER_HUB_CREDENTIALS_PSW | docker login --username $DOCKER_HUB_CREDENTIALS_USR --password-stdin
                    docker push chatlearning123/getting-started:latest
                    '''
                }
            }
        }
    }
}
