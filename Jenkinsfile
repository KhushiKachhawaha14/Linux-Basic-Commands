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
                echo 'Running tests... (Intentionally failing now)'
                
                // 🛑 NEW STEP: FORCE BUILD FAILURE 
                // This command will exit with a status of 1 (failure).
                // Jenkins interprets any non-zero exit status as a failure,
                // stopping subsequent stages and triggering the 'post { failure }' block.
                sh 'exit 1' 
                
                // Alternatively, you could use the native Groovy step:
                // error('Intentionally failing the Test stage.')
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
            // ✅ THIS BLOCK WILL BE EXECUTED
            echo 'Build failed! Sending failure email...'
            mail to: 'khushimushu@gmail.com',
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
