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
                echo 'Building the project...'
                sh 'npm run build'
            }
        }
        stage('Deploy to render') {
            steps {
                echo 'Deploying the application...'
                sh 'node server.js'
            }
        }
    }
     post {
        always {
            echo 'Pipeline finished.'
        }
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
