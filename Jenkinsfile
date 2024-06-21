pipeline {
    agent any

    stages {
        stage('Setup Python Environment') {
            steps {
                script {
                    echo 'Setting up Python environment...'
                    sh 'python3 -m venv venv'
                    sh '. venv/bin/activate && pip install --upgrade pip'
                }
            }
        }

        stage('Lint') {
            steps {
                script {
                    echo 'Checking code indentation...'
                    sh '. venv/bin/activate && pip install flake8'
                    sh '. venv/bin/activate && flake8 app.py'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh '. venv/bin/activate && pip install pytest'
                    sh '. venv/bin/activate && pytest --maxfail=1 --disable-warnings -q'
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
                    sh '. venv/bin/activate && python app.py'
                }
            }
        }
    }
}
