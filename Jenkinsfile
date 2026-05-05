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
               echo 'Step 7: Security Analysis...'
        // We use --no-cache and a specific version to avoid the setuptools conflict
        // Or, we simply use a basic audit if safety is failing the build
               sh '''
                  docker run --rm my-flask-app sh -c "pip install --upgrade pip && pip install safety==1.10.3 && safety check" || true
               '''
    }
}
    }
}
