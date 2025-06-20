pipeline {
    agent any

    environment {
        SONARQUBE = 'LocalSonar'
    }

    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/naveen2729/SonarQube.git'
            }
        }

        stage('Install') {
            steps {
                dir('myproject') {
                    bat 'npm install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('myproject') {
                    withSonarQubeEnv("${SONARQUBE}") {
                        bat 'sonar-scanner.bat'
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('jenkins-docker-demo')
                }
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 3000:3000 jenkins-docker-demo'
            }
        }
    }
}
