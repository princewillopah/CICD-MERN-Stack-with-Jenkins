// pipeline {
//     agent any
//     tools {
//         nodejs "node16"
//     }
//     environment {
//         SCANNER_HOME=tool 'sonar-scanner' // define path of sonarqube scanner tool //'sonar-scanner' is the name we specified in tool
//     }
//     stages {
//         stage('Git Checkout') { 
//             steps {
//                 git credentialsId: 'git-credentials', url: 'https://github.com/princewillopah/CICD-MERN-Stack-with-Jenkins'
//             }
//         }

//         stage('Install Backend Dependencies') { 
//             steps {
//                 dir('AppFiles/Backend') {
//                     sh "npm install"
//                 }
//             }
//         }

//         stage('Install Frontend Dependencies') { 
//             steps {
//                 dir('AppFiles/Frontend') {
//                     sh "npm install"
//                 }
//             }
//         }

//         stage('Unit Test Backend') { 
//             steps {
//                 // dir('AppFiles/Backend') {
//                 //     sh "npm test"
//                 // }
//                 echo 'Backend Test Completed'
//             }
//         }

//         stage('Unit Test Frontend') { 
//             steps {
//                 // dir('AppFiles/Frontend') {
//                 //     sh "npm test"
//                 // }
//                  echo 'Frontend Test Completed'
//             }
//         }

//         stage('Trivy FS Scan') { 
//             steps {
//                 sh "trivy fs --format table -o trivy-fs-report.html ." // scanning the whole repository
//             }
//         }

//         stage('SonarQube') { 
//             steps {
//                 withSonarQubeEnv('sonarqube-server') { 
//                     sh ''' 
//                     $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=CICD-MERN-Stack-with-Jenkins \
//                     -Dsonar.projectKey=CICD-MERN-Stack-with-Jenkins
//                     '''
//                 }
//             }
//         }        
        
//         stage("Docker Build & Tag Backend"){
//             steps{
//                 script{
//                     withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){   
//                         dir('AppFiles/backend') {
//                             sh "docker build -t princewillopah/CICD-MERN-Stack-with-Jenkins-Backend:v-1.0.1 ."
//                         }
//                     }
//                 }
//             }
//         }

//         stage("Docker Build & Tag Frontend"){
//             steps{
//                 script{
//                     withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){   
//                         dir('AppFiles/frontend') {
//                             sh "docker build -t princewillopah/CICD-MERN-Stack-with-Jenkins-Frontend:v-1.0.1 ."
//                         }
//                     }
//                 }
//             }
//         }

//         stage("Trivy Image Scan Backend"){
//             steps{
//                 sh "trivy image --format table -o trivy-backend-image-report.html princewillopah/CICD-MERN-Stack-with-Jenkins-Backend:v-1.0.1" 
//             }
//         }

//         stage("Trivy Image Scan Frontend"){
//             steps{
//                 sh "trivy image --format table -o trivy-frontend-image-report.html princewillopah/CICD-MERN-Stack-with-Jenkins-Frontend:v-1.0.1" 
//             }
//         }

//         stage("Push Backend To DockerHub"){
//             steps{
//                 script{
//                     withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){ 
//                         sh "docker push princewillopah/CICD-MERN-Stack-with-Jenkins-Backend:v-1.0.1"
//                     }
//                 }
//             }
//         }

//         stage("Push Frontend To DockerHub"){
//             steps{
//                 script{
//                     withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){ 
//                         sh "docker push princewillopah/CICD-MERN-Stack-with-Jenkins-Frontend:v-1.0.1"
//                     }
//                 }
//             }
//         }

//         // stage("Deploy Backend To Dev"){
//         //     steps{
//         //         script{
//         //             withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){ 
//         //                 sh "docker run -d -p 5000:5000 princewillopah/backend:v-1.0.1"
//         //             }
//         //         }
//         //     }
//         // }

//         // stage("Deploy Frontend To Dev"){
//         //     steps{
//         //         script{
//         //             withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){ 
//         //                 sh "docker run -d -p 3000:3000 princewillopah/frontend:v-1.0.1"
//         //             }
//         //         }
//         //     }
//         // }
//     }
// }


pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'
    }
    stages {
        stage('Test Docker Access') {
            steps {
                script {
                    sh 'docker ps'
                }
            }
        }
        stage('Docker Login') {
            steps {
                script {
                    withDockerRegistry(credentialsId: DOCKER_CREDENTIALS_ID) {
                        sh 'docker info'
                    }
                }
            }
        }
    }
}
