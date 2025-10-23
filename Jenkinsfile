pipeline {
    agent any // Defines where the pipeline will run (any available agent)

    stages {
        stage('Fetch Code from Git') {
            steps {
                // 1. Fetch Data from Git using the 'checkout' or 'git' step
                git branch: 'main', 
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
        // Send a detailed email ONLY on build success
        success {
            echo "Build successful. Sending success notification email."
            mail to: 'khushimushu@gmail.com', 
                subject: "\$PROJECT_NAME - Build #\$BUILD_NUMBER - SUCCESS",
                body: """
                    <h2>Jenkins Build Notification: SUCCESS</h2>
                    <p>Job: \$PROJECT_NAME (Build #\$BUILD_NUMBER)</p>
                    <p>Status: SUCCESS</p>
                    <p>Check the full details here: <a href="\$BUILD_URL">View Console Output</a></p>
                    
                    <h3>Changes in this Build:</h3>
                    <ul>
                        \$CHANGES_SINCE_LAST_SUCCESS // Fetches and displays commit details from Git
                    </ul>
                """
        
        }

        // Send an urgent email ONLY on build failure
        failure {
            echo "Build failed. Sending urgent failure email."
            mail to: 'khushimushu@gmail.com', // Different recipient for failure
                subject: "\$PROJECT_NAME - Build #\$BUILD_NUMBER - FAILURE",
                body: """
                    <h2>Jenkins Build Notification: FAILURE</h2>
                    <p>Job: \$PROJECT_NAME (Build #\$BUILD_NUMBER)</p>
                    <p>Status: FAILURE - Please investigate immediately.</p>
                    <p>Error details: <a href="\$BUILD_URL">View Console Output and Stack Trace</a></p>
                """
            
        }

        // Always run cleanup steps, regardless of build result
        always {
            echo "Performing post-build cleanup actions."
            // sh 'rm -rf build' // Example cleanup command
        }
    }
}

                

  

             
                
