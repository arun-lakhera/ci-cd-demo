pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'                      // SonarQube ka URL
        SONAR_AUTH_TOKEN = credentials('sonar-token')                 // Jenkins credentials store se secure token fetch
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/arun-lakhera/ci-cd-demo.git'
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


