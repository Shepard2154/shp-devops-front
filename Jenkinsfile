pipeline {
    agent any;

    stages {
        stage('install deps') {
            steps {
                sh 'npm install';
            }
        }

        stage('build') {
            steps {
                sh 'npm run build_prod';
            }
        }
    }
}