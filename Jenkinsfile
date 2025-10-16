pipeline {
    environment {
<<<<<<< Updated upstream
        registry = "NourhenHamza/spring-boot-devops"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }

    agent any

=======
        registry = "NourhenHamza/spring-boot-pipeline"
        registryCredential = 'github-access'
        dockerImage = ''
    }
    agent any
>>>>>>> Stashed changes
    stages {
        stage('CHECKOUT GIT') {
            steps {
                git 'https://github.com/NourhenHamza/spring-boot-devops.git';
            }
        }
<<<<<<< Updated upstream

=======
>>>>>>> Stashed changes
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
<<<<<<< Updated upstream

=======
>>>>>>> Stashed changes
        stage('UNIT TESTS') {
            steps {
                echo 'launching Unit Tests...'
                sh 'mvn test'
            }
        }
<<<<<<< Updated upstream

=======
>>>>>>> Stashed changes
        stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
            }
        }
<<<<<<< Updated upstream

=======
>>>>>>> Stashed changes
        stage("PUBLISH TO NEXUS") {
            steps {
                sh 'java -version'
            }
        }
<<<<<<< Updated upstream

=======
>>>>>>> Stashed changes
        stage('BUILDING OUR IMAGE') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    sh 'java -version'
                }
            }
        }
<<<<<<< Updated upstream

=======
>>>>>>> Stashed changes
        stage('DEPLOY OUR IMAGE') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                        sh 'java -version'
                    }
                }
            }
        }
    }
}