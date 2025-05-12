pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/TejasPatil75/flask-ci-demo.git'
            }
        }

        stage('Setup Environment') {
            steps {
                bat """
                python -m venv %VENV%
                call %VENV%\\Scripts\\activate
                pip install -r requirements.txt
                """
            }
        }

        stage('Run Tests') {
            steps {
                bat """
                call %VENV%\\Scripts\\activate
                pytest
                """
            }
        }

        stage('Run App') {
            steps {
                bat """
                call %VENV%\\Scripts\\activate
                start /B python app.py
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
