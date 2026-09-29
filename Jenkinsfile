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
                echo 'Testing application...'

                sh '''
                    test -f index.html
                    test -f style.css
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r ./* /var/www/html/
                '''
            }
        }

        stage('Verify') {
            steps {
                echo 'Checking deployment...'

                sh '''
                    test -f /var/www/html/index.html
                    test -f /var/www/html/style.css
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