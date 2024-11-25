pipeline {
    agent any
    tools {
        nodejs "nodejs" // Use the name defined in Global Tool Configuration
    }
    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Build') {
            steps {
                echo 'No build step required.'
                sh 'npm run build' 
                }
                
     }
        stage('Deploy to Render') {
          steps {
        echo 'Deploying the application...'
        // Run the server in the background using nohup 
        sh '''
        nohup node server.js &
        '''
    }
        }
    }
     post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            script {
                echo 'Pipeline completed successfully!'
                // Slack notification for success
                withCredentials([string(credentialsId: 'slack-bot-token', variable: 'SLACK_TOKEN')]) {
                    slackSend(
                        channel: '#hamsa_ip1',
                        tokenCredentialId: 'slack-bot-token', // Use the credential ID directly here
                        color: 'good',
                        message: "Pipeline completed successfully! 🎉\nBuild ID: ${currentBuild.id}\nView your deployed application here: https://gallery-l0ph.onrender.com"
                    )
                }
            }
        }
        failure {
            script {
                // Send email in case of failure
                emailext to: 'hamsa.adan1@student.moringaschool.com',
                         subject: "Build Failed",
                         body: "The Jenkins build has failed. Please check the logs for more details."
                // Slack notification for failure
                withCredentials([string(credentialsId: 'slack-bot-token', variable: 'SLACK_TOKEN')]) {
                    slackSend(
                        channel: '#hamsa_ip1',
                        tokenCredentialId: 'slack-bot-token', // Use the credential ID directly here
                        color: 'danger',
                        message: "Pipeline failed. 🚨\nBuild ID: ${currentBuild.id}\nPlease check the Jenkins logs for details."
                    )
                }
            }
        }
    }
}
