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
                bat 'docker build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
                bat 'docker tag %IMAGE_NAME%:%BUILD_NUMBER% %IMAGE_NAME%:latest'
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Mengirim Docker image ke registry...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'docker login -u %USER% -p %PASS%'
                    bat 'docker push %IMAGE_NAME%:%BUILD_NUMBER%'
                    bat 'docker push %IMAGE_NAME%:latest'
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

### Langkah Penanganan:

1. Buka file **`Jenkinsfile`** di repository GitHub milikmu (`praktikum_simple-app`).
2. Klik ikon **Edit (Pensil)**, **hapus seluruh isi file lama**, lalu **replace/paste** dengan kode utuh di atas.
3. Klik **Commit changes...** di GitHub.
4. Kembali ke Jenkins, klik **Build Now**[cite: 7].

*(Catatan Tambahan: Jika build masih gagal, kamu bisa klik nomor build misal **#31** di menu sebelah kiri $\rightarrow$ pilih **Console Output** untuk melihat pesan error spesifik dari Jenkins).*
