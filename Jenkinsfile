pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling app.py...'
                // Simulating compilation check
                bat 'python -m py_compile app.py'
                
                echo 'Waiting 15 seconds...'
                sleep time: 15, unit: 'SECONDS'
                
                echo 'Passing milestone 1...'
                milestone(1)
            }
        }

        stage('Send Notification') {
            steps {
                script {
                    def recipient = 'developer@example.com'
                    def mailSubject = "Build Notification: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}"
                    def mailBody = "The build finished successfully. Review details here: ${env.BUILD_URL}"
                    
                    try {
                        // Attempt standard SMTP notification
                        mail to: recipient,
                             subject: mailSubject,
                             body: mailBody
                        echo "Notification email sent successfully to ${recipient}."
                    } catch (Exception e) {
                        // Workaround fallback if SMTP server setup is missing
                        echo "[SMTP Workaround Log Alert]"
                        echo "To: ${recipient}"
                        echo "Subject: ${mailSubject}"
                        echo "Body: ${mailBody}"
                    }
                }
            }
        }
    }
}
