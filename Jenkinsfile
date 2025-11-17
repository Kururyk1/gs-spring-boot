pipeline {
    agent any

    stages {

        stage('Clone repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Kururyk1/gs-spring-boot.git'
            }
        }

        stage('Build Spring Boot app') {
            steps {
                sh 'mvn clean package'
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

