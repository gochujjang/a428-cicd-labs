node {
    def dockerImage = 'node:16-buster-slim'
    def dockerPort = '-p 3000:3000'

    options {
        pipelineTriggers([
            pollSCM('*/2 * * * *')
        ])
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