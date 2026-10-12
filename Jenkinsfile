pipeline {
    agent any

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
                echo 'Membangun Docker image...'
                bat '"C:\\Users\\farrelaudric\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t farrelaudric/praktikum_simple-app:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Mengirim Docker image ke registry...'
                bat '"C:\\Users\\farrelaudric\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" push farrelaudric/praktikum_simple-app:latest'
            }
        }
    }

    post {
        always {
            echo 'Selesai build 🏁'
        }
    }
}
