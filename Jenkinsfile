pipeline {
    agent any // Defines where the pipeline will run (any available agent)

    stages {
        stage('Fetch Code from Git') {
            steps {
                // 1. Fetch Data from Git using the 'checkout' or 'git' step
                git branch: 'main', 
                    credentialsId: 'KhushiKachhawaha14', // Replace with the ID of your Git credentials (SSH Key or Username/Password)
                    url: 'https://github.com/KhushiKachhawaha14/Linux-Basic-Commands.git' // Replace with your repository URL

                // Optional: Print details about the last commit for verification
                sh 'echo "Last commit details:"'
                sh 'git log -1 --pretty=format:"%h - %an, %ar : %s"' 
            }
        }
        
        stage('Build/Test') {
            steps {
                // Placeholder for your actual project work (e.g., compile, run tests)
                echo "Simulating a build step..." 
                // sh './mvnw clean install' // Example command
            }
        }
    }

    // 2. Send Email Notifications using the 'post' section
    post {
        // Always attempt to send an email, regardless of the stage results
        always {
            echo "Checking build status for email notification..."
            
            // Use the Email Extension Plugin step 'emailext'
            emailext (
                // Email recipients (use space, comma, or semi-colon separated list)
                to: 'dev.team@example.com', 
                
                // Subject line will be customized based on the status
                subject: "\$PROJECT_NAME - Build #\$BUILD_NUMBER - \$BUILD_STATUS",
                
                // HTML body content
                body: """
                    <h2>Jenkins Build Notification: \$BUILD_STATUS</h2>
                    <p>Job: \$PROJECT_NAME (Build #\$BUILD_NUMBER)</p>
                    <p>Status: \$BUILD_STATUS</p>
                    <p>Check the full details here: <a href="\$BUILD_URL">View Console Output</a></p>
                    
                    <h3>Changes in this Build:</h3>
                    <ul>
                        \$CHANGES_SINCE_LAST_SUCCESS // Fetches and displays commit details from Git
                    </ul>
                """,
                // Triggers define which build statuses send an email
  // ... (Your Stages block ends)
// }  <-- This brace closes the 'stages' block

post { // <--- The 'post' block starts here
    always {
        // ... actions for all build results
    }

    // Line 67 is here, correctly inside the 'post' block
    failure {
        echo "Build failed. Sending urgent failure email."
        // Add a separate email configuration here if you want different recipients/c
    }
} // <--- The 'post' block closes here
// }  <-- This brace closes the entire 'pipeline' block
