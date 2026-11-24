
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building website...'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing website...'
                sh 'test -f index.html'
                sh 'grep -q "Welcome to My Automatic CI/CD Pipeline!" index.html'
                echo 'All tests passed!'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website to Nginx...'
                sh 'cp index.html /var/www/html/index.html'
                echo 'Deployment successful!'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'curl -fsS http://localhost/ | grep -q "Welcome to My Automatic CI/CD Pipeline!"'
                echo 'Deployment verification passed!'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
