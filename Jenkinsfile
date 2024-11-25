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
        sh '''
            nohup node server.js &
            sleep 60  # Wait for 60 seconds (or as needed)
            kill $(jobs -p)  # Kill the background process after timeout
        '''
    }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            script {
                // Send email in case of failure
                emailext to: 'hamsa.adan1@student.moringaschool.com',
                         subject: "Build Failed",
                         body: "The Jenkins build has failed. Please check the logs for more details."
            }
        }
    }
}
