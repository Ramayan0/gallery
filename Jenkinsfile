pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
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
}
