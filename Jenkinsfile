pipeline {
    agent any

    stages {
        stage('Setup Python Environment') {
            steps {
                script {
                    echo 'Setting up Python environment...'
                    sh 'python3 -m venv venv'
                    sh './venv/bin/pip install --upgrade pip'
                }
            }
        }

        stage('Lint') {
            steps {
                script {
                    echo 'Checking code indentation...'
                    sh './venv/bin/pip install flake8'
                    sh './venv/bin/flake8 app.py'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh './venv/bin/pip install pytest'
                    sh './venv/bin/pytest --maxfail=1 --disable-warnings -q'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    sh 'echo "Build successful!"'
                }
            }
        }

        stage('Run') {
            steps {
                script {
                    echo 'Running the application...'
                    sh './venv/bin/python app.py'
                }
            }
        }
    }
}
