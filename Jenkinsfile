pipeline {
    environment {
        registry = "nourhenhamza/spring-boot-devops"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any
    
    tools {
        maven 'Maven'
    }
    
    stages {
        stage('CHECKOUT GIT') {
            steps {
                git branch: 'master',
                    url: 'https://gitlab.com/ThourayaLouati/docker-spring-boot.git'
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
                echo 'Launching Unit Tests...'
                sh 'mvn test'
            }
        }
        
        stage('MVN SONARQUBE') {
            steps {
                echo 'Running SonarQube Analysis...'
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
            }
        }
        
        stage("PUBLISH TO NEXUS") {
            steps {
                echo 'Publishing to Nexus...'
                sh 'java -version'
            }
        }
        
        stage('BUILDING DOCKER IMAGE') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }
        
        stage('DEPLOY DOCKER IMAGE') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                        dockerImage.push('latest')
                    }
                }
            }
        }
        
        stage('CLEANUP') {
            steps {
                script {
                    sh "docker rmi ${registry}:${BUILD_NUMBER}"
                    sh "docker rmi ${registry}:latest"
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline execution failed!'
        }
        always {
            cleanWs()
        }
    }
}