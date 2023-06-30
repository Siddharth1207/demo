pipeline {
    environment {
        registry = "siddharth1207/learning"
        registryCredential = 'dockerhub-credentials'
        dockerImage = ''
    }
    agent any

    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/Siddharth1207/demo.git'
            }
        }

        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build(registry + ":$BUILD_NUMBER")
                }
            }
        }

        stage('Deploy our image') {
            steps {
                script {
                    withDockerRegistry(url: "", credentialsId: registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
