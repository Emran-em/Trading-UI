pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Git checkout') {
            steps {
                git 'https://github.com/Emran-em/Trading-UI.git'
            }
        }

        stage('Install npm prerequisites') {
            steps {
                // npm ci is better for CI/CD (clean install, uses package-lock.json)
                sh 'npm ci'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                # Stop existing PM2 process if running
                pm2 delete Trading-UI || true
                # Start new instance
                pm2 --name Trading-UI start npm -- start
                '''
            }
        }
    }

    post {
        always {
            // Optional: clean workspace instead of just node_modules
            cleanWs()
        }
    }
}
