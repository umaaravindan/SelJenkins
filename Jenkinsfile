stage('Build-push Docker Image') {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/umaaravindan/Selenium_Trial.git']])
                    def dockerfile = 'Dockerfile'
                    def imageTag = "martinmartin234/vuejs-foot" 
                    def customImage = docker.build(imageTag, "-f ${dockerfile} ./")
                    
                    docker.withRegistry('', 'dockercon') {
                        customImage.push()
                    }
                }
            }
        }

