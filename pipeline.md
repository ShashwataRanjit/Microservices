pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/ShashwataRanjit/Microservices.git'
            }
        }

        stage('Build & Push Docker Images') {
            steps {
                sh '''
                chmod +x Microservices/docker_image_buid_push.sh
                ./Microservices/docker_image_buid_push.sh
                '''
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh '''
                kubectl apply -f Microservices/kubernetes-manifests
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                kubectl get pods
                '''
            }
        }
    }
}