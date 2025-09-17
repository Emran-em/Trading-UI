pipeline {
    agent any

    tools {
        nodejs "NodeJS14"   // ✅ Make sure Jenkins is configured with NodeJS under Global Tools
    }

    stages {
        stage('Git checkout') {
            steps {
                // ✅ Checkout from GitHub
                git branch: 'master', url: 'https://github.com/betawins/Trading-UI.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                  rm -rf node_modules package-lock.json   # ✅ clean install
                  npm install --omit=optional
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                  npm run build
                '''
            }
        }

        stage('Run with PM2') {
            steps {
                sh '''
                  cd build
                  pm2 delete Trading-UI || true   # ✅ delete if already running
                  pm2 start npm --name "Trading-UI" -- start
                '''
            }
        }
    }

    post {
        success { echo '✅ Build and deployment completed successfully!' }
        failure { echo '❌ Pipeline failed — check logs.' }
    }
}
