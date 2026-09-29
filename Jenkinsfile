pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting code from GitHub...'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Checking application files...'

                bat '''
                    if not exist index.html exit /b 1
                    if not exist style.css exit /b 1
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                bat '''
                    if not exist C:\\JenkinsDeploy mkdir C:\\JenkinsDeploy
                    xcopy /E /Y /I . C:\\JenkinsDeploy
                '''
            }
        }

        stage('Verify') {
            steps {
                echo 'Verifying deployment...'

                bat '''
                    if not exist C:\\JenkinsDeploy\\index.html exit /b 1
                    if not exist C:\\JenkinsDeploy\\style.css exit /b 1
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}