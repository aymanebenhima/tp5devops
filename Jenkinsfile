pipeline {
    agent any
    environment {
        registry = "aymanebenhima/tp5devops"
        registryCredential = 'dockerhub'
    }
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/aymanebenhima/tp5devops.git'
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy image') {
            steps {
                script {
                    sh "docker run -d --name tp4-app -p 80:80 $registry:$BUILD_NUMBER"
                }
            }
        }
    }
}