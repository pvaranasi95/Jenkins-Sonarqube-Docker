pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/pvaranasi95/Jenkins-Sonarqube-Docker.git']])
            }
        }
        // stage('Sonar scan') {
        //     steps{
        //         script{
        //         bat 'cd C:\\Users\\pavan\\OneDrive\\Desktop\\sonarqube-10.4.1.88267\\sonar-scanner-6.1.0.4477-windows-x64\\bin'
        //        bat 'C:\\Users\\pavan\\OneDrive\\Desktop\\sonarqube-10.4.1.88267\\sonar-scanner-6.1.0.4477-windows-x64\\bin\\sonar-scanner.bat -D"sonar.projectKey=Jenkins-Sonarqube-Docker" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.token=sqp_3a7c14cc0030612ec004f1f554f6fa17fd9298a3"'
        //          }
        //     }
        // }
    //     stage('Docker Image') {
    //         steps{
    //             bat 'docker build -t pvaranasi/onixweb:%BUILD_NUMBER% .'
    //         }
    //     }
    //     stage('Docker Push') {
    //         steps{
    //             bat 'docker push pvaranasi/onixweb:%BUILD_NUMBER%'
    //         }
    //     }
    //     stage('Container') {
    //         steps{
    //             bat 'docker run -d -p 8088:80 --name onixweb-%BUILD_NUMBER% pvaranasi/onixweb:%BUILD_NUMBER%'
    //         }
    //     }
    // }
    post{
        always{
            script {
                    def jenkinsBuildData = [
                job_name: env.JOB_NAME,
                build_number: env.BUILD_NUMBER.toInteger(),
                status: currentBuild.currentResult,
                timestamp: new Date().format("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", TimeZone.getTimeZone('UTC')),
                duration: currentBuild.duration,
                url: env.BUILD_URL
            ]

            def jsonBody = groovy.json.JsonOutput.toJson(jenkinsBuildData)
            def jsonBodyEscaped = jsonBody.replace('"', '\\"')

            echo "Sending build data to Elasticsearch: ${jsonBody}"

            bat """
            curl.exe -X POST "http://localhost:9200/jenkins/_doc" ^
                 -H "Content-Type: application/json" ^
                 -d "${jsonBodyEscaped}"
            """
                }

        }
    }
}
}
