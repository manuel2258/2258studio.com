pipeline {
    environment {
        registry = "manuel2258/2258studio"
        registryCredential = "dockerhub"
    }
    agent { docker { image 'jekyll/builder' } }
    stages {
        stage('build site') {
            steps {
                checkout scm
                sh 'bundle exec jekyll build'
            }
        }
        stage('build docker image') {
            steps {
                script {
                    docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
    }
}