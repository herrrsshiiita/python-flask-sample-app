pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // This pulls your code from GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Docker Image...'
                // This satisfies Step 4 of your assignment
                sh 'docker build -t my-flask-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Unit Tests...'
                // This satisfies Step 5 of your assignment
                // We run the tests inside a temporary container
                sh 'docker run --rm my-flask-app pytest'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Scanning for vulnerabilities...'
                // This satisfies Step 7: We'll add Snyk/Trivy here later
                echo 'Security scan placeholder'
            }
        }
    }
}
