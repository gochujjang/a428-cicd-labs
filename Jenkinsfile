node {
    def dockerImage = 'node:16-buster-slim'
    def dockerPort = '-p 3000:3000'

    stage('Checkout'){
        docker.image(dockerImage).inside(dockerPort) {
            echo 'Checkout scm'
            checkout scm
        }
    }

    stage('Build') {
        docker.image(dockerImage).inside(dockerPort) {
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
}