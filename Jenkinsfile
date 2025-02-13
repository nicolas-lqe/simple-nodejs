pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "lisandrodev/simple-nodejs"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/LisandroLuna/simple-nodejs.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER} ."
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh "sudo docker run --rm ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER} npm test"
                }
            }
        }

    //     stage('Push Docker Image') {
    //         steps {
    //             script {
    //                 withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
    //                     sh "echo ${DOCKER_HUB_PASSWORD} | sudo docker login -u ${DOCKER_HUB_USERNAME} --password-stdin"
    //                     sh "sudo docker push ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER}"
    //                     sh "sudo docker tag ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER} ${DOCKER_IMAGE_NAME}:latest"
    //                     sh "sudo docker push ${DOCKER_IMAGE_NAME}:latest"
    //                 }
    //             }
    //         }
    //     }
    // }

    // post {
    //     always {
    //         script {
    //             try {
    //                 sh "sudo docker rmi ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER}"
    //             } catch (Exception e) {
    //                 echo 'Failed to remove Docker image.'
    //             }
    //         }
    //     }
    }
}
