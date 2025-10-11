pipeline {
    agent any
    
    environment {
        registry = "nourhen-spring-boot-app"
    }

    stages {
        stage('CHECKOUT GIT') {
            steps {
                git branch: 'develop', 
                    url: 'https://github.com/NourhenHamza/spring-boot-devops.git'
            }
        }

        stage('ARTIFACT CONSTRUCTION') {
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }

        stage('BUILD DOCKER IMAGE') {
            steps {
                script {
                    docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution completed'
        }
    }
}