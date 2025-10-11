pipeline {
    agent {
        docker {
            image 'maven:3.8.5-openjdk-17'
            args '-v /root/.m2:/root/.m2'
        }
    }
    
    environment {
        registry = "NourhenHamza/spring-boot-devops"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }

    stages {
        stage('CHECKOUT GIT') {
            steps {
                git branch: 'develop', 
                    url: 'https://github.com/NourhenHamza/spring-boot-devops.git'
            }
        }

        stage('MVN CLEAN') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('ARTIFACT CONSTRUCTION') {
            steps {
                echo 'ARTIFACT CONSTRUCTION...'
                sh 'mvn package -Dmaven.test.skip=true -P test-coverage'
            }
        }

        stage('UNIT TESTS') {
            steps {
                echo 'launching Unit Tests...'
                sh 'mvn test'
            }
        }

        stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.host.url=http://host.docker.internal:9000 -Dsonar.login=admin -Dsonar.password=nourhen123'
            }
        }

        stage("PUBLISH TO NEXUS") {
            steps {
                sh 'java -version'
            }
        }

        stage('BUILDING OUR IMAGE') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('DEPLOY OUR IMAGE') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}