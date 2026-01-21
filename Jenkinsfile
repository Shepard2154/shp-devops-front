pipeline {
    agent any;

    environment {
        PROJECT_PATH = '/var/www/burnaev'
    }

    stages {
        stage('install deps') {
            steps {
                sh 'npm install';
            }
        }

        stage('build') {
            steps {
                sh 'npm run build_prod';
                sh 'cp -r dist/ ${PROJECT_PATH}';
            }
        }

    }
}