
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

        stage('Backup') {
            steps {
                echo 'Creating previous version backup...'
                sh '''
                    if [ -f /var/www/html/index.html ]; then
                        cp /var/www/html/index.html /var/backups/jenkins/index.html
                    fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website...'
                sh 'cp index.html /var/www/html/index.html'
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
        failure {
            echo 'Deployment failed. Restoring previous version...'
            sh '''
                if [ -f /var/backups/jenkins/index.html ]; then
                    cp /var/backups/jenkins/index.html /var/www/html/index.html
                fi
            '''
        }
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }
    }
}
