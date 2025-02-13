pipeline {
    agent any
    environment {
        registry = "udiorgad/my_jenkins"  // The name of your Docker Hub repository
        registryCredential = "docker_hub" // The credentials ID stored in Jenkins
        dockerImage = "" // Will be assigned dynamically
    }
    
    stages {
        stage('Build and Push Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}") // Name and version the image
                    echo dockerImage
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push() // Push image to Docker Hub
                    }
                }
            }
        }
    }
    
    post {
        always {
            script {
                \\bat "docker rmi ${registry}:${BUILD_NUMBER}" // Delete the local image at the end
            }
        }
    }
}
