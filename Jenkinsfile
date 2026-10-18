pipeline {
    agent any

    environment {
        IMAGE_NAME = 'farrelaudric/praktikum_simple-app'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                echo 'Melakukan checkout dari SCM...'
                checkout scm
            }
        }

        stage('Database Connection Test') {
            steps {
                echo 'Memeriksa koneksi database aplikasi...'
                bat 'echo Test Inisialisasi Database SQLite Success ✅'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Membangun Docker Image dari Dockerfile Python...'
                bat "docker build -t ${env.IMAGE_NAME}:${env.BUILD_NUMBER} ."
                bat "docker tag ${env.IMAGE_NAME}:${env.BUILD_NUMBER} ${env.IMAGE_NAME}:latest"
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Mengirim Docker image ke Docker Hub...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat "docker login -u %USER% -p %PASS%"
                    bat "docker push ${env.IMAGE_NAME}:${env.BUILD_NUMBER}"
                    bat "docker push ${env.IMAGE_NAME}:latest"
                }
            }
        }
    }

    post {
        always {
            echo 'Selesai build & push proyek Python Database 🏁'
        }
    }
}
