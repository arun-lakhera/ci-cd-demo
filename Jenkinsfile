pipeline {
    agent any

    tools {
        sonarScanner 'SonarQubeScanner'  // Global Tool Config में दिया गया नाम
    }

    environment {
        SONAR_AUTH_TOKEN = credentials('sonar-token')   // Jenkins credentials में दिया गया ID
        SONAR_HOST_URL = 'http://localhost:9000'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/arun-lakhera/ci-cd-demo.git'
            }
        }

        stage('Print Token') {
            steps {
                echo "Token is: ${SONAR_AUTH_TOKEN}"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=ci-cd-demo \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=${SONAR_HOST_URL} \
                          -Dsonar.login=${SONAR_AUTH_TOKEN}
                    '''
                }
            }
        }
    }
}

