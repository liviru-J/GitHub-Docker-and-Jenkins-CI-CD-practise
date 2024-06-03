pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/liviru-J/GitHub-Docker-and-Jenkins-CI-CD-practise'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t liviru/nodeapp-test:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'test-dockerhubpassword', variable: 'testdockerhubpass')]) {
                    bat "docker login -u liviru -p ${testdockerhubpass}"
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push liviru/nodeapp-test:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
