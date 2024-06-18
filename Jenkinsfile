pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-2' // Replace with your AWS region
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Fetch Secret') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'awscred']]) {
                    script {
                        // Fetch the secret from AWS Secrets Manager
                        def secret = sh(
                            script: 'aws secretsmanager get-secret-value --secret-id test-secret --query SecretString --output text',
                            returnStdout: true
                        ).trim()
                        
                        // Print the secret
                        echo "Fetched secret: ${secret}"
                    }
                }
            }
        }
    }
}
