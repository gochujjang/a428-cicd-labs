node {
    def dockerImage = 'node:16-buster-slim'
    def dockerPort = '-p 3000:3000'

    stage('Build') {
        docker.image(dockerImage).inside(dockerPort) {
            checkout scm
            echo 'Running npm install'
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image(dockerImage).inside(dockerPort) {
            echo 'Running test.sh'
            sh './jenkins/scripts/test.sh'
        }
    }

    stage('Manual Approval') {
        docker.image(dockerImage).inside(dockerPort) {
            input message: 'Lanjut ke tahap Deploy? (Klik "Proceed" jika ingin melakukan deployment)'
        }
    }

    stage('Deploy') {
        docker.image(dockerImage).inside(dockerPort) {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh 'sleep 1m'
            sh './jenkins/scripts/kill.sh'
        }
    }
}