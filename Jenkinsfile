pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Install dependencies
                sh 'pip install -r requirements.txt'
                // Build the Docker image
                sh 'docker build -t web-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Run tests
                sh 'pytest'
            }
        }

        stage('Vulnerability Scan') {
            steps {
                echo 'Scanning for vulnerabilities...'
                // Run Trivy scan
                sh 'trivy image web-app'
            }
        }
    }
}
