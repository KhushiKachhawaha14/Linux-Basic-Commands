pipeline {
    agent any
    
    // Set environment variables for easy maintenance
    environment {
        EMAIL_RECIPIENTS = 'khushimushu@gmail.com'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'echo "Build step completed"'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests (Intentionally forcing failure now)'
                // This command exits with status 1, marking the build as FAILURE
                sh 'exit 1' 
            }
        }

        stage('Deploy') {
            steps {
                echo 'This stage is skipped due to failure in the Test stage.'
            }
        }
    }

    post {
        failure {
            echo 'Build failed! Executing post-failure actions and sending email.'
            
            mail to: "${env.EMAIL_RECIPIENTS}",
                // Use currentBuild.fullDisplayName for a clean job name and build number
                subject: "❌ Build FAILED: ${currentBuild.fullDisplayName}",
                body: """
                <h3>⚠️ Build Failed!</h3>
                <p>Project: ${env.JOB_NAME}</p>
                <p>Build Number: ${env.BUILD_NUMBER}</p>
                <p>Status: FAILURE</p>
                
                <!-- This link must point to the globally configured Jenkins URL -->
                <p>Check the logs here: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                
                <p>Note: If the link above does not work, the Jenkins URL is configured incorrectly in Manage Jenkins > System.</p>
                """,
                mimeType: 'text/html'
        }
    }
}
