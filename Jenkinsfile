pipeline {
    agent { docker { image 'jekyll/builder' } }
    stages {
        stage('build') {
            steps {
                sh 'jekyll build'
                sh 'docker build -t manuel2258/jekyll .'
            }
        }
        stage('deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}