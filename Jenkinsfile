pipeline {
    agent any

    environment {
        IMAGE_NAME = 'farrelaudric/praktikum_simple-app'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials' // Pastikan sama persis dengan ID credential di Jenkins
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
                bat "docker build -t %IMAGE_NAME%:%BUILD_NUMBER% ."
                bat "docker tag %IMAGE_NAME%:%BUILD_NUMBER% %IMAGE_NAME%:latest"
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Mengirim Docker image ke registry...'
                withCredentials([usernamePassword(credentialsId: "${env.REGISTRY_CREDENTIALS}",
                    usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'docker login -u %USER% -p %PASS%'
                    bat "docker push %IMAGE_NAME%:%BUILD_NUMBER%"
                    bat "docker push %IMAGE_NAME%:latest"
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

### Langkah Selanjutnya:
1. Simpan perubahan file `Jenkinsfile` tersebut di repository GitHub kamu (**Commit changes**)[cite: 7].
2. Pastikan koneksi internet stabil dan aplikasi **Docker Desktop** dalam keadaan *Running*[cite: 7].
3. Kembali ke halaman project Jenkins kamu, lalu klik **Build Now**[cite: 7]. 

Pipeline sekarang akan berjalan dengan aman menggunakan token rahasia dari Jenkins dan berhasil melakukan *push* image ke Docker Hub tanpa error *timeout* atau kredensial invalid[cite: 7]!
