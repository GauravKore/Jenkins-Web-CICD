pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'

                git branch: 'main',
                    url: 'https://github.com/GauravKore/Jenkins-Web-CICD.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Build: Checking project files...'

                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo 'Test: Validating required files...'

                bat 'if exist index.html (echo index.html found) else (exit /b 1)'
                bat 'if exist style.css (echo style.css found) else (exit /b 1)'
                bat 'if exist script.js (echo script.js found) else (exit /b 1)'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application to IIS...'

                bat 'xcopy /Y /I index.html "%DEPLOY_DIR%\\"'
                bat 'xcopy /Y /I style.css "%DEPLOY_DIR%\\"'
                bat 'xcopy /Y /I script.js "%DEPLOY_DIR%\\"'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
            echo 'Website: http://localhost/index.html'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}