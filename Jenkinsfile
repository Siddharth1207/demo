pipeline {
    agent any
    environment {
        registry = "siddharth1207/learning"
        registryCredential = 'siddharth1207'
        dockerImage = ''
    }
    stages {
        stage('Cloning our Git') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Siddharth1207/demo.git']])
            }
        }
        stage('Building our image') {
            steps {
                script {
					sh 'docker build -t Kirti_image .'
                   
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
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
