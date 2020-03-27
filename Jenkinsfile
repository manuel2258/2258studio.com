pipeline {
    environment {
        registry = "manuel2258/2258studio"
        registryCredential = "dockerhub"
    }
    agent any
    stages {
        stage('Deploy docker image') {
            agent any
            steps {
                sh 'ssh root@79.143.179.92 "cd /home/manuel/docker; docker-compose up -d;"'
            }
        }
        stage('Build site') {
            agent { docker { image 'jekyll/builder' } }
            steps {
                sh 'bundle update'
                sh 'bundle install'
                sh 'bundle exec jekyll build'
            }
        }

        stage('Build docker image') {
            agent any
            steps {
                script {
                    dockerImage = docker.build registry + ":latest"
                }
            }
        }
        stage('Upload docker image') {
            agent any
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}