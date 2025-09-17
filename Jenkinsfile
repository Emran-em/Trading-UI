pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git 'https://github.com/Emran-em/Trading-UI.git'
            }
        }
        stage('Install npm prerequisites') {
            steps {
                sh '''
                    rm -rf node_modules package-lock.json
                    npm install
                    npm audit fix || true
                    npm run build
                    cd build
                    pm2 --name Trading-UI start npm -- start
                '''
            }
        }
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
