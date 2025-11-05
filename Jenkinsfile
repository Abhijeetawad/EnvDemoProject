pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['DIT', 'SIT', 'UAT', 'PRODUCTION'],
            description: 'Select environment to build and deploy'
        )
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Abhijeetawad/EnvDemoProject.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building project for ${params.ENVIRONMENT} environment..."
            }
        }

        stage('Test') {
            steps {
                echo "Running tests for ${params.ENVIRONMENT} environment..."
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENVIRONMENT} environment..."
            }
        }
    }

    post {
        success {
            echo "✅ Build successful for ${params.ENVIRONMENT}!"
        }
        failure {
            echo "❌ Build failed for ${params.ENVIRONMENT}!"
        }
    }
}
