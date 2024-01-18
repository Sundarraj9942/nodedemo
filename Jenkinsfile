pipeline {
    agent any 

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }

    stages {
        stage('SCM Checkout') {
            steps {
                sh 'rm -rf Sundar@994 || true'  // Remove existing directory if it exists
                sh 'git clone https://github.com/Sundarraj9942/nodedemo.git'
                echo 'test1'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'test2'
                sh 'docker build -t raj9942/Sundar@994:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    }
                    echo 'test3'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push raj9942/Sundar@994:latest'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
