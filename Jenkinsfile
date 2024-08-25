pipeline {
    agent {
        node{label 'Windows1'}
    }
    tools {
        jdk 'JDK11'  //JDK17
        maven 'Maven'
    }

    stages {
        stage('Git checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/pvaranasi95/Jenkins-Sonarqube-Docker.git']])
            }
        }
        stage('Sonar scan') {
            steps{
                script{
                bat 'cd C:\\Users\\pavan\\OneDrive\\Desktop\\sonarqube-10.4.1.88267\\sonar-scanner-6.1.0.4477-windows-x64\\bin'
               bat 'C:\\Users\\pavan\\OneDrive\\Desktop\\sonarqube-10.4.1.88267\\sonar-scanner-6.1.0.4477-windows-x64\\bin\\sonar-scanner.bat -D"sonar.projectKey=Jenkins-Sonarqube-Docker" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.token=sqp_3a7c14cc0030612ec004f1f554f6fa17fd9298a3"'
                 }
            }
        }
    }
}
