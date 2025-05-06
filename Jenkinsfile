pipeline {
    agent any

    tools {
        sonarScanner 'SonarQubeScanner'   // Jenkins Global Tool Config me add kiya hua name
    }

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'             // SonarQube ka URL
        SONAR_AUTH_TOKEN = sqa_1757b1e7fbb9ad0eff6ae777cb17005a5d35b3b2        // Jenkins me add kiya hua token ID
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

