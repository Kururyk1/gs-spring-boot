pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                git 'https://github.com/Kururyk1/gs-spring-boot.git'
            }
        }

        stage('Build Spring Boot app') {
            steps {
                sh './gradlew clean build'
            }
        }
    }

    post {
        success {
            echo "BUILD SUCCESS – JAR CREATED!"
        }
        failure {
            echo "BUILD FAILED"
        }
    }
}

                                                                                
