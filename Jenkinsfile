pipeline {
    agent any

    stages {
        stage('Setup Python Environment') {
            steps {
                script {
                    echo 'Setting up Python environment...'
                    sh 'python3 -m venv venv'
                    sh './venv/bin/pip install --upgrade pip'
                    sh './venv/bin/pip install -r requirements.txt'
                }
            }
        }

        stage('Lint') {
            steps {
                script {
                    echo 'Checking code indentation...'
                    sh './venv/bin/flake8 app.py'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running unit tests...'
                    sh './venv/bin/pytest --maxfail=1 --disable-warnings -q'
                }
            }
        }

        stage('Verify App URL') {
            steps {
                script {
                    echo 'Verifying Flask application URL...'

                    // Replace with your Flask app URL and port
                    def appUrl = 'http://localhost:5000/'

                    // Use curl to make an HTTP request and capture the response code
                    def responseCode = sh(returnStatus: true, script: "curl -s -o /dev/null -w '%{http_code}' ${appUrl}")

                    if (responseCode == '200') {
                        echo "Flask application is running fine. Response code: ${responseCode}"
                    } else {
                        error "Failed to verify Flask application URL. Response code: ${responseCode}"
                    }
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
                    sh './venv/bin/python app.py &'
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Stopping the application...'
                sh 'pkill -f "python app.py"'
            }
        }
    }
}