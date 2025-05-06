pipeline {
    agent any

    environment {
        SONAR_AUTH_TOKEN = credentials('sonar-token')   // Jenkins credentials ID
        SONAR_HOST_URL = 'http://localhost:9000'        // SonarQube server URL
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
                withSonarQubeEnv('SonarQube') {  // 'SonarQube' is the name you configured in Jenkins
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

