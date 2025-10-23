pipeline {
    agent any
    
    environment {
        // Email recipients (you'll usually replace with real emails or a param)
        EMAIL_RECIPIENTS = 'khushimushu@gmail.com'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the project... (Successful)'
                sh 'echo "Simulating build process..."'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests... (Intentionally failing now to test email)'
                
                // This command will exit with a status of 1 (failure), 
                // stopping subsequent stages and triggering the 'post { failure }' block.
                sh 'exit 1' 
                
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application... (This stage will be skipped)'
                sh 'echo "Deployment completed!"'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded! (This will not run as we forced a failure)'
        }

        failure {
            // ✅ THIS BLOCK WILL BE EXECUTED because the 'Test' stage failed.
            echo 'Build failed! Sending failure email via standard mail step...'
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
