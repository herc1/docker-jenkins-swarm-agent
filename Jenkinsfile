pipeline {
    agent { label 'docker-agent' }
    stages {
        stage('build') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE_NAME}:${env.BUILD_ID}")
                }
            }
        }
        stage('push') {
            steps {
                script {
                    docker.withRegistry('https://registry-1.docker.io/v2/', 'dockerHubCredentials') {
                        dockerImage.push()
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}