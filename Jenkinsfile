pipeline {
    agent any
    environment {
        IMAGE_NAME = 'abdieeeuh/simple-app'
        REGISTRY = 'https://index.docker.io/v1/'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Melakukan checkout dari SCM...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Mulai build aplikasi'
                bat 'echo Build selesai ✅'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Membangun Docker image...'
                    // Mengarahkan langsung ke file executable docker milik user di AppData
                    bat "\"C:\\Users\\farrelaudric\\AppData\\Local\\Programs\\Docker\\Docker\\resources\\bin\\docker.exe\" build -t ${IMAGE_NAME}:${env.BUILD_NUMBER} ."
                    echo "Image berhasil dibuat: ${IMAGE_NAME}:${env.BUILD_NUMBER}"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    echo 'Push image ke Docker Hub...'
                    docker.withRegistry(REGISTRY, REGISTRY_CREDENTIALS) {
                        bat "\"C:\\Users\\farrelaudric\\AppData\\Local\\Programs\\Docker\\Docker\\resources\\bin\\docker.exe\" push ${IMAGE_NAME}:${env.BUILD_NUMBER}"
                        bat "\"C:\\Users\\farrelaudric\\AppData\\Local\\Programs\\Docker\\Docker\\resources\\bin\\docker.exe\" tag ${IMAGE_NAME}:${env.BUILD_NUMBER} ${IMAGE_NAME}:latest"
                        bat "\"C:\\Users\\farrelaudric\\AppData\\Local\\Programs\\Docker\\Docker\\resources\\bin\\docker.exe\" push ${IMAGE_NAME}:latest"
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Selesai build 🏁OYYY'
        }
    }
}
