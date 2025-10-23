pipeline {
    agent any                      // run on any available agent/node

    environment {
        // Email recipients (you'll usually replace with real emails or a param)
        EMAIL_RECIPIENTS = 'khushimushu@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Example build step
                sh 'echo "Simulating build process..."'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Example test command
                sh 'echo "Tests successful!"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh 'echo "Deployment completed!"'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded! Sending success email...'
            mail to: 'khushimushu@gmail.com',
                subject: "Jenkins Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h3>✅ Build Successful!</h3>
                <p>Project: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p>Check the build details: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                mimeType: 'text/html'
    
        }

        failure {
            echo 'Build failed! Sending failure email...'
            mail to: "${env.EMAIL_RECIPIENTS}",
                subject: "❌ Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h3>⚠️ Build Failed!</h3>
                <p>Project: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p>Check the logs here: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                mimeType: 'text/html'
            
        }
    }
}
             
                
