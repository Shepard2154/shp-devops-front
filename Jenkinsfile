pipeline {
    agent any;

    environment {
        PROJECT_PATH = '/var/www/burnaev'
        CONF_PATH = '/etc/nginx/sites-available/burnaev_front.conf'
        CONF_NAME = 'burnaev_front.conf'
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
                        listen 443 ssl;
                        server_name burnaev.mshptop.ru;

                        location / {
                            root ${PROJECT_PATH};
                            try_files \\\$uri /index.html;
                        }

                        ssl_certificate /etc/letsencrypt/live/burnaev.mshptop.ru/fullchain.pem;
                        ssl_certificate_key /etc/letsencrypt/live/burnaev.mshptop.ru/privkey.pem;
                        include /etc/letsencrypt/options-ssl-nginx.conf;
                        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
                    }" > ${CONF_PATH}
                """;
                sh  "ln -sf ${CONF_PATH} /etc/nginx/sites-enabled/${CONF_NAME}";
            }
        }

    }
}