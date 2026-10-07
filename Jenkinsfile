pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mkdir -p build'
                sh 'cp index.html build/index.html'
                echo 'Build completed successfully.'
            }
        }

        stage('Test') {
            steps {
                sh 'test -f build/index.html'
                sh 'grep -q "DevOps Lab 1" build/index.html'
                echo 'Test passed successfully.'
            }
        }

        stage('Deploy') {
            steps {
                sh 'mkdir -p deployed/app'
                sh 'cp build/index.html deployed/app/index.html'
                sh 'echo "Deployment completed at $(date)" > deployed/deployment.log'
                sh 'ls -la deployed/app'
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully.'
        }
        failure {
            echo 'CI/CD pipeline failed.'
        }
    }
}
