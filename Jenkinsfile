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

        stage('Verify App URL') {
            steps {
                script {
                    echo 'Verifying Flask application URL...'
                    def appUrl = 'http://172.17.0.2:5000/'
                    def responseCode = sh(returnStdout: true, script: "curl -s -o /dev/null -w '%{http_code}' ${appUrl}")
                    echo "Response code: ${responseCode.trim()}"

                    if (responseCode.trim() == '200') {
                        echo "Flask application is running fine."
                    } else {
                        error "Failed to verify Flask application URL. Response code: ${responseCode.trim()}"
                    }
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