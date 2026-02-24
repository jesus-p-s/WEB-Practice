pipeline {
    agent any

    stages {

        stage('Input data') {
            input {
                message 'Enter deployment info'
                parameters {
                    string(name:'AUTHOR', defaultValue: 'Sergio', description: 'Author of the deployment')
                    string(name:'ENVIRONMENT', defaultValue: 'Development', description: 'Environment to deploy')
                }
            }
            steps {
                echo "Responsible: ${AUTHOR} | Environment: ${ENVIRONMENT}"
            }
        }

        stage('Prepare web files') {
            steps {
                echo 'Copying web files to Docker volume...'
                // Crear el volumen si no existe
                sh 'docker volume create webdata || true'
                // Limpiar contenido anterior
                sh 'docker run --rm -v webdata:/data alpine sh -c "rm -rf /data/*"'
                // Copiar archivos del workspace al volumen
                sh 'docker run --rm -v webdata:/data -v ${WORKSPACE}/web:/src alpine sh -c "cp -r /src/. /data/"'
            }
        }

        stage('Recreate Apache container') {
            steps {
                echo 'Dropping and recreating Apache container...'
                // Eliminar contenedor si existe
                sh 'docker rm -f apache1 || true'
                // Crear nuevo contenedor Apache con el volumen correcto
                sh '''
                docker run -dit \
                  --name apache1 \
                  -p 9001:80 \
                  -v webdata:/usr/local/apache2/htdocs \
                  httpd
                '''
                // Ajustar permisos
                sh 'docker exec apache1 chown -R www-data:www-data /usr/local/apache2/htdocs'
                sh 'docker exec apache1 chmod -R 755 /usr/local/apache2/htdocs'
            }
        }

        stage('Check web app') {
            steps {
                echo 'Testing the web app...'
                // Esperar un poco para que Apache arranque
                sh 'sleep 5'
                sh 'curl -f http://host.docker.internal:9001'
            }
        }
    }
}
