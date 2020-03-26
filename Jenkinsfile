pipeline {
    environment {
        registry = "manuel2258/2258studio"
        registryCredential = "dockerhub"
    }
    agent any
    stages {
        stage('Build site') {
            steps {
                checkout scm
            }
        }

        stage('Build docker image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy docker image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}