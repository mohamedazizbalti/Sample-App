pipeline {
    agent any

    environment {
        IMAGE_NAME = "sample-app"
        DOCKER_REGISTRY = "medazizbalti1"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_REGISTRY}/${IMAGE_NAME}")
                }
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Run your tests here (e.g., npm test, pytest, etc.)'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerhub-creds', url: '' ]) {
                    script {
                        docker.image("${DOCKER_REGISTRY}/${IMAGE_NAME}").push("latest")
                    }
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    sh "docker rmi ${DOCKER_REGISTRY}/${IMAGE_NAME}"
                }
            }
        }
    }
}
