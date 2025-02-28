pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Create and activate virtual environment
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate'
                // Install dependencies within the virtual environment
                sh 'venv/bin/pip install -r requirements.txt'
                // Build the Docker image
                sh 'docker build -t web-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Run tests within the virtual environment
                sh 'venv/bin/pytest'
            }
        }

        stage('Vulnerability Scan') {
            steps {
                echo 'Scanning for vulnerabilities...'
                // Ensure Trivy is installed
                sh 'curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh'
                // Run Trivy scan
                sh 'trivy image web-app'
            }
        }
    }

    post {
        always {
            // Deactivate virtual environment (optional)
            sh 'deactivate'
        }
    }
}
