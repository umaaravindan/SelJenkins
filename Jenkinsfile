pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'
        DOCKER_IMAGE = 'chatlearning123/getting-started:latest'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${env.DOCKER_IMAGE}", ".")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                        dockerImage.push()
                        sh 'docker logout'
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
