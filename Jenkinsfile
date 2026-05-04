pipeline {
    agent any
    
    // This tells Jenkins to use the Docker tool you configured in 'Manage Jenkins'
    environment {
        DOCKER_API_VERSION = '1.40'
    }
    tools {
        dockerTool 'docker' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Running Docker Build...'
                // 'sh' is the command that actually does the work
                sh 'docker build -t my-flask-app .'
            }
        }

        stage('Test') {
    steps {
        echo 'Installing and Running Unit Tests...'
        // This installs pytest first, THEN runs it
        sh 'docker run --rm my-flask-app sh -c "pip install pytest && pytest"'
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
