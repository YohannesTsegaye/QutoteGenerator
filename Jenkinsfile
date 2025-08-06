pipeline {
    agent any

    tools {
        nodejs 'NodeJS'
    }

    environment {
        SCANNER_HOME = tool 'SonarQubeScanner'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/rohitbharti258/QutoteGenerator.git', branch: 'main'
            }
        }
        stage('Install & Build') {
            steps {
                sh 'npm install'
                // optional: run unit tests if present, e.g. `npm test`
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('MySonarQube') {
                    sh "${SCANNER_HOME}/bin/sonar-scanner"
                }
            }
        }
    }

    post {
        success {
            echo 'Analysis complete – check SonarQube dashboard.'
        }
        failure {
            echo 'Pipeline failed. Check Jenkins console logs.'
        }
    }
}
