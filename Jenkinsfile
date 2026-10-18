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

### Langkah Eksekusi:
1. Edit file **`Jenkinsfile`** langsung di GitHub, *paste* kode di atas, lalu klik **Commit changes**.
2. Pastikan aplikasi **Docker Desktop** di Windows dalam keadaan aktif (*Running*).
3. Kembali ke dashboard Jenkins, lalu klik tombol **Build Now**[cite: 7].

Dengan perbaikan ini, error pencarian path direktori `HP` akan hilang, proses build image akan berhasil, dan tahap *push* ke Docker Hub kamu akan berjalan mulus!
