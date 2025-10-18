pipeline {
    agent any
    // Define the trigger for the pipeline
    triggers {
        githubPush() // This is part of the GitHub Plugin
    }
    stages {
        stage('Checkout Code') {
            steps {
                // The pipeline automatically checks out the code from the SCM defined in the job configuration
                echo "Checking out code..."
                // You can explicitly check out if needed, but often unnecessary for Multibranch Pipeline
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Building the application..."
                // Example: Execute a Maven build command
                // sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                // Example: Execute a test script
                // sh './run_tests.sh'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying to environment..."
            }
        }
    }
}
