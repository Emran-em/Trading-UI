pipeline {
    agent any

    tools {
        nodejs "NodeJS16"   // Must match the name in Jenkins config
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Emran-em/Trading-UI.git'
            }
        }

        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }
}
