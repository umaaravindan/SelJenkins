pipeline {
    agent {
        docker {
            image 'maven:3.6.3-jdk-8'
            label 'docker-agent'
            args '-v /root/.m2:/root/.m2'
        }
    }
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_REPO = 'chatlearning123/getting-started'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry("https://${DOCKER_REGISTRY}", 'dockerhub-credentials') {
                        def app = docker.build("${DOCKER_REPO}:${env.BUILD_ID}")
                        app.push()
                    }
                }
            }
        }
    }
}
