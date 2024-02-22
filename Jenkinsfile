pipeline {
    agent any 

    environment {
        DOCKERHUB_CREDENTIALS = credentials('sss')
    }

    stages {
        stage('SCM Checkout') {
            steps {
                sh 'rm -rf sundar || true'  // Remove existing directory if it exists
                sh 'git clone https://github.com/Sundarraj9942/sampledemo.git'
                echo 'test1'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'test2'
                sh 'docker build -t raj9942/sundar:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'sss', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        sh "docker login -u raj9942 -p Sundar@994"
                    }
                    echo 'test3'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push raj9942/sundar:latest'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
