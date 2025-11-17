pipeline {
    agent any
    
environment {
    NEXUS_REPO = "http://localhost:8081/repository/r-maven/"
    NEXUS_CREDENTIALS = credentials('nexus-admin')
}


    stages {

        stage('Clone repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Kururyk1/gs-spring-boot.git'
            }
        }

        stage('Build Spring Boot app') {
            steps {
                dir('complete') {
                    withMaven(maven: 'maven') {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    def jarFile = sh(
                        script: "ls complete/target/*.jar",
                        returnStdout: true
                    ).trim()

                    sh """
                    curl -v -u ${NEXUS_CREDENTIALS_USR}:${NEXUS_CREDENTIALS_PSW} \
                    --upload-file ${jarFile} \
                    ${NEXUS_REPO}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "ARTIFACT UPLOADED TO NEXUS SUCCESSFULLY!"
        }
        failure {
            echo "UPLOAD FAILED — CHECK LOGS"
        }
    }
}
