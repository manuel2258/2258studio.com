pipeline {
    environment {
        registry = "gustavoapolinario/docker-test"
        registryCredential = ‘dockerhub’
    }
    agent { docker { image 'jekyll/builder' } }
    stages {
        stage('build site') {
            steps {
                checkout scm
                sh 'jekyll build'
            }
        }
        stage('build docker image') {
            steps {
                docker.build registry + ":$BUILD_NUMBER"
            }
        }
    }
}