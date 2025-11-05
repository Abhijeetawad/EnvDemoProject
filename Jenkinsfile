pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['DIT', 'SIT', 'UAT', 'PRODUCTION'],
            description: 'Select deployment environment'
        )
    }

    environment {
        DIT_URL  = "http://dit.example.com"
        SIT_URL  = "http://sit.example.com"
        UAT_URL  = "http://uat.example.com"
        PROD_URL = "http://prod.example.com"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Fetching source code from GitHub..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building project for ${params.ENVIRONMENT} environment..."
                bat 'javac src/envdemo/HelloJenkins.java'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (params.ENVIRONMENT == 'DIT') {
                        echo "Deploying to DIT environment at ${env.DIT_URL}"
                    } else if (params.ENVIRONMENT == 'SIT') {
                        echo "Deploying to SIT environment at ${env.SIT_URL}"
                    } else if (params.ENVIRONMENT == 'UAT') {
                        echo "Deploying to UAT environment at ${env.UAT_URL}"
                    } else {
                        echo "Deploying to Production at ${env.PROD_URL}"
                    }
                }
            }
        }

        stage('Post-Deployment') {
            steps {
                echo "✅ Deployment to ${params.ENVIRONMENT} completed successfully!"
            }
        }
    }

    post {
        always {
            echo "Cleaning workspace..."
            cleanWs()
        }
    }
}
