pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/madarameegama7/CI-CD-Pipeline-with-Docker-and-Jenkins'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t damithrimeegama/pipeline-creation:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'test-dockerhubpass')]){
                        bat "docker login -u damithrimeegama -p %test-dockerhubpass%"
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push damithrimeegama/pipeline-creation:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
