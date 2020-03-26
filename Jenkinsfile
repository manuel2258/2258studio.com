Jenkinsfile (Declarative Pipeline)
pipeline {
    agent { docker { image 'jekyll/builder' } }
    stages {
        stage('build') {
            steps {
                sh 'jekyll build'
            }
        }
    }
}