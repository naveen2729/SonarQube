pipeline {
    agent any

    environment {
        SONARQUBE = 'LocalSonar' // Must match name in Jenkins -> Manage Jenkins -> SonarQube servers
    }

    tools {
        nodejs 'NodeJS' // Must match your NodeJS tool name
        sonarScanner 'SonarScanner' // Optional if you configured SonarScanner in Jenkins
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/naveen2729/SonarQube.git'
            }
        }

        stage('Install') {
            steps {
                bat 'npm install'
            }
        }

        stage('Check Sonar Scanner') {
            steps {
                bat 'where sonar-scanner'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    bat 'sonar-scanner.bat'
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
