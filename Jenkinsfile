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

       stage('Code Quality') {
            steps {
                echo 'Step 6: Static Code Analysis (Linting)...'
                sh 'docker run --rm my-flask-app sh -c "pip install flake8 && flake8 . --ignore=E501,F401"'
            }
        }

        stage('Test') {
            steps {
                echo 'Step 5: Unit Testing...'
                sh 'docker run --rm my-flask-app sh -c "pip install pytest && pytest"'
            }
        }

       stage('Security Scan') {
    steps {
        echo 'Step 7: Identifying and Blocking Critical Vulnerabilities...'
        // We use 'docker run' to enter the container where 'pip' actually exists
        sh 'docker run --rm my-flask-app sh -c "pip install safety && safety check --ignore 84961"'
    }
}
    }
}
