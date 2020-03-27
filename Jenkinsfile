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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'local', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'cd /home/manuel/docker; docker-compose up -d', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
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
                    docker.withRegistry('', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}