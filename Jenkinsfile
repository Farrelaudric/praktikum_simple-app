pipeline {
    agent any

    environment {
        IMAGE_NAME = 'farrelaudric/praktikum_simple-app'
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
                echo 'Membangun Docker image...'
                bat "docker build -t ${env.IMAGE_NAME}:${env.BUILD_NUMBER} ."
                bat "docker tag ${env.IMAGE_NAME}:${env.BUILD_NUMBER} ${env.IMAGE_NAME}:latest"
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Mengirim Docker image ke registry...'
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
            echo 'Selesai build 🏁'
        }
    }
}
```[cite: 7]

---

### Langkah Mengecek Detail Error (Penting)

Jika setelah mengganti `Jenkinsfile` build berikutnya masih gagal, kamu bisa melihat **alasan persis kegagalannya** dengan cara:

1. Di panel sebelah kiri under menu **Builds**, klik angka build terbaru (misalnya **#35**)[cite: 10].
2. Klik menu **Console Output**[cite: 7].
3. Lihat bagian paling bawah log terminal tersebut untuk mengetahui baris mana yang menyebabkan error[cite: 7].

Silakan di-commit dulu perubahan `Jenkinsfile` di atas lalu klik **Build Now**[cite: 7]!
