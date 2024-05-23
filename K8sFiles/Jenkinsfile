pipeline {
    agent any
    tools {
        nodejs "node16"
    }
     environment {
         SCANNER_HOME=tool 'sonar-scanner'  // define path of sonarqube scanner tool //'sonar-scanner' is the name we specified in tool
     }
    stages {
        stage('Git Checkout') { 
            steps {
                git credentialsId: 'git-credentials', url: 'https://github.com/princewillopah/CICD-MERN-Stack-with-Jenkins'
            }
        }

        stage('Install Package Dependencies') { // 
            steps {
                sh "npm install"
            }
        }

        stage('Unit Test') { // 
            steps {
                sh "npm test"
            }
        }

        stage('Trivy FS Scan') { // trivy to perform file system scan // note that we didn't define trivy in the pipeline unlike nodejs. this is because we installed trivy directly in the jenkins server
            steps {// this will run the analysis and export results to separate file "trivy-fs-report.html"
                  sh "trivy fs --format table -o trivy-fs-report.html ." // trivy fs will scan the current directory specified by "." and present the results in tabular format in a file trivy-fs-report.html
            }
        }

        stage('SonarQube') { // 
            steps {
                withSonarQubeEnv('sonarqube-server') {  // call the sonarqube server we configured in system //    withSonarQubeEnv(credentialsId: 'sonar-token') {}
                 sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=CICD-MERN-Stack-with-Jenkins \
                     -Dsonar.projectKey=CICD-MERN-Stack-with-Jenkins '''
                }
            }
        }        
          stage("Docker Build & Tag"){
             steps{
                 script{
                    withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){   
                        sh "docker build -t princewillopah/cicd-mern-stack-with-jenkins:v-1.0.1 ."
                     }
                 }
             }
         }
         stage("Trivy Image Scan"){
             steps{
                 sh "trivy image  --format table -o trivy-image-report.html princewillopah/cicd-mern-stack-with-jenkins:v-1.0.1" 
             }
         }

          stage("Push To DockerHub"){
             steps{
                 script{
                    withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){ 
                        sh "docker push princewillopah/cicd-mern-stack-with-jenkins:v-1.0.1"
                     }
                 }
             }
         }

        stage("Deploy To Dev"){
             steps{
                 script{
                    withDockerRegistry(credentialsId: 'dockerhub-credentials', toolName: 'docker'){ 
                        sh "docker run -d -p 3000:3000 "
                     }
                 }
             }
         }
        // stage('  ') { // 
        //     steps {
                
        //     }
        // }

        // stage('  ') { // 
        //     steps {
                
        //     }
        // }

        // stage('  ') { // 
        //     steps {
                
        //     }
        // }        

        // stage('  ') { // 
        //     steps {
                
        //     }
        // }
        // stage('  ') { // 
        //     steps {
                
        //     }
        // }

        // stage('  ') { // 
        //     steps {
                
        //     }
        // }

        // stage('  ') { // 
        //     steps {
                
        //     }
        // }        

        // stage('  ') { // 
        //     steps {
                
        //     }
        // }        


    }
}