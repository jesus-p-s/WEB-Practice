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

        stage('Recreate Apache container') {
            steps {
                echo 'Dropping and recreating Apache container...'
                // Eliminar contenedor si existe
                sh 'docker rm -f apache1 || true'
                // Crear contenedor Apache vacío
                sh 'docker run -dit --name apache1 -p 9001:80 httpd'
            }
        }

        stage('Copy web application into container') {
            steps {
                echo 'Copying web files into Apache container...'
                // Copiar los archivos directamente al contenedor
                sh 'docker cp ${WORKSPACE}/web/. apache1:/usr/local/apache2/htdocs/'
                // Ajustar permisos dentro del contenedor
                sh 'docker exec apache1 chown -R www-data:www-data /usr/local/apache2/htdocs'
                sh 'docker exec apache1 chmod -R 755 /usr/local/apache2/htdocs'
            }
        }

        stage('Check web app') {
            steps {
                echo 'Testing the web app...'
                sh 'sleep 5'
                sh 'curl -f http://host.docker.internal:9001'
            }
        }
    }
}
