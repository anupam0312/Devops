pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/anupam0312/Devops.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Artifact') {
            steps {
                sh '''
                    zip -r build.zip . -x "node_modules/*" ".git/*" "Jenkinsfile"
                '''
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build.zip', fingerprint: true
            }
        }

        stage('Notify') {
            steps {
                echo '✅ Build and test completed successfully! (Mock notification: Slack/Email)'
            }
        }
    }

    post {
        failure {
            echo "❌ Build failed! (Mock notification: Slack/Email)"
        }
    }
}
