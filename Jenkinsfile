pipeline {
    agent any
    // Add this environment block to help Jenkins find Docker
    environment {
        DOCKER_HOME = '/usr/bin/docker'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // This pulls your code from GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // This uses the Docker plugin logic instead of a raw shell command
                    docker.build("my-flask-app:${env.BUILD_ID}")
                }
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
