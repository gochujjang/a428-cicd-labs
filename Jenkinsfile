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
    docker.image(dockerImage).withRun('-p 3000:3000') {
        stage('Build') {
            sh 'apt-get update && apt-get install -y nodejs npm'
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
    }
}