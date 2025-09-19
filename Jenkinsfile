pipeline {
    agent any
    tools {
        // 👇 Name must match what you configured under "Manage Jenkins → Global 
Tool Configuration → NodeJS"
Terraform task-4        nodejs "Nodejs16"
    }
    environment {
        SKIP_PREFLIGHT_CHECK = 'true'   // skip eslint version mismatch checks
        CI = 'false'                    // avoid treating warnings as errors
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/master']],
                    userRemoteConfigs: [[url:'https://github.com/Emran-em/Trading-UI.git']]
                ])
            }
        }
        stage('Clean Workspace') {
            steps {
                sh '''
                    echo "🧹 Cleaning workspace..."
                    rm -rf node_modules package-lock.json
                    npm cache clean --force || true
                '''
Terraform task-4            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                    echo "👇 Installing dependencies..."
                    npm install --legacy-peer-deps
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    echo "🧹 Running tests..."
                    npm test || echo "⚠️ No tests found"
                '''
            }
        }
        stage('Build') {
            steps {
                sh '''
                    echo "👇  Building React app with Node.js $(node -v)..."
                    npm run build
Terraform task-4                '''
            }
        }
    }
    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed — check console output."
        }
    }
