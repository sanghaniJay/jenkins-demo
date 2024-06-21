pipeline {
    agent any

    stages {
        stage('Lint') {
            steps {
                script {
                    echo 'Checking code indentation...'
                    sh 'pip install flake8'
                    sh 'flake8 app.py'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'pip install -r requirements.txt'
                    sh 'pytest --maxfail=1 --disable-warnings -q'
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
                    sh 'python app.py'
                }
            }
        }
    }
}
