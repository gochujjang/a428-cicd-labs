// pipeline {
//     agent {
//         docker {
//             image 'node:16-buster-slim' 
//             args '-p 3000:3000' 
//         }
//     }
//     stages {
//         stage('Build') { 
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh './jenkins/scripts/test.sh'
//             }
//         }
//     }
// }

// Scripted Pipeline
node {
    def dockerImage = 'node:16-buster-slim'
    def dockerPort = '-p 3000:3000'

    stage('Checkout'){
        docker.image(dockerImage).withRun(dockerPort) {
            checkout scm
        }
    }

    stage('Build') {
        docker.image(dockerImage).withRun(dockerPort) {
            checkout scm
            echo 'Running npm install'
            sh 'npm install'
        }
    }

    stage('Test') {
        docker.image(dockerImage).withRun(dockerPort) {
            echo 'Running test.sh'
            sh './jenkins/scripts/test.sh'
        }
    }
}