pipeline {
    agent {
        docker {
            image 'dokceruma'
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
                git 'https://github.com/umaaravindan/SelJenkins.git'
                echo 'GIT CHEKPOUT DONE'
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
