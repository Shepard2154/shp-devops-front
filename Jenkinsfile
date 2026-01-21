pipeline {
    agent any;

    environment {
        PROJECT_PATH = '/var/www/burnaev'
        CONF_PATH = '/etc/nginx/sites-available/burnaev_front.conf'
        CONF_NAME = 'burnaev_front.conf'
        NGINX_PORT = '80'
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
                sh """echo "server {
                        listen ${NGINX_PORT};
                        server_name mshptop.ru;

                        location / {
                            root ${PROJECT_PATH};
                            try_files \\\$uri /index.html;
                        }
                    }" > ${CONF_PATH}
                """;
                sh  "ln -sf ${CONF_PATH} /etc/nginx/sites-enabled/${CONF_NAME}";
            }
        }

    }
}