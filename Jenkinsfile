pipeline {
    agent any

    parameters {
        choice(name: 'ENVIRONMENT', choices: ['DIT', 'SIT', 'UAT', 'PRODUCTION'], description: 'Select environment')
    }

    stages {
        stage('Detect Environment') {
            steps {
                script {
                    // Detect if ENVIRONMENT is pre-set by the job (DIT, SIT, etc.)
                    if (!params.ENVIRONMENT) {
                        env.ENVIRONMENT = 'DIT'
                    }
                    echo "Running build for environment: ${params.ENVIRONMENT}"
                }
            }
        }

        stage('Build') {
            steps {
                echo "Building for ${params.ENVIRONMENT}"
                bat 'javac src/envdemo/HelloJenkins.java'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENVIRONMENT} environment"
            }
        }
    }
}
