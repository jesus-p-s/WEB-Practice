pipeline {
    agent any

    environment {
        WEB_VOLUME = "webdata"
        APACHE_CONTAINER = "apache1"
        APACHE_PORT = "9001"
    }

    stages {
        stage('Create Docker volume') {
            steps {
                echo "Creating shared Docker volume for web files..."
                sh """
                docker volume inspect ${WEB_VOLUME} >/dev/null 2>&1 || \
                docker volume create ${WEB_VOLUME}
                """
            }
        }

        stage('Input deployment data') {
            input {
                message 'Enter deployment data'
                parameters {
                    string(name:'AUTHOR', defaultValue: 'Sergio', description: 'Author of the deployment')
                    string(name:'ENVIRONMENT', defaultValue: 'Development', description: 'Environment to deploy')
                }
            }
            steps {
                echo "Responsible: ${AUTHOR} | Environment: ${ENVIRONMENT}"
            }
        }

        stage('Copy web application') {
            steps {
                echo 'Copying web application to Docker volume...'
                sh """
                docker run --rm -v ${WEB_VOLUME}:/data alpine sh -c 'rm -rf /data/*'
                docker run --rm -v ${WEB_VOLUME}:/data -v \$(pwd)/web:/src alpine sh -c 'cp -r /src/. /data/'
                """
            }
        }

        stage('Recreate Apache container') {
            steps {
                echo 'Dropping and recreating Apache container...'
                sh """
                docker rm -f ${APACHE_CONTAINER} || true
                docker run -dit \
                    --name ${APACHE_CONTAINER} \
                    -p ${APACHE_PORT}:80 \
                    -v ${WEB_VOLUME}:/usr/local/apache2/htdocs \
                    httpd
                docker exec ${APACHE_CONTAINER} chown -R www-data:www-data /usr/local/apache2/htdocs
                docker exec ${APACHE_CONTAINER} chmod -R 755 /usr/local/apache2/htdocs
                """
            }
        }

        stage('Check web app') {
            steps {
                echo 'Testing the web app...'
                sh 'sleep 5'
                sh "curl -f http://host.docker.internal:${APACHE_PORT}"
            }
        }
    }
}
