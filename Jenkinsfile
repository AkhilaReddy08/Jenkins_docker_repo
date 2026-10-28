pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AkilaReddy08/jenkins-docker-deployment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myweb:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f myweb-container || true
                    docker run -d \
                        --name myweb-container \
                        --restart unless-stopped \
                        -p 8092:80 \
                        myweb:${BUILD_NUMBER}
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
                sh 'curl -f http://localhost:8092'
            }
        }
    }
}
