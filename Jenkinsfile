pipeline {
    environment {
        registry = "manuel2258/2258studio"
        registryCredential = "dockerhub"
    }
    agent any
    stages {
        stage('Build site') {
            agent { docker { image 'jekyll/builder' } }
            steps {
                checkout scm
                sh 'bundle update'
                sh 'bundle install'
                sh 'bundle exec jekyll build'
            }
        }

        stage('Build docker image') {
            agent any
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy docker image') {
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