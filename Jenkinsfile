pipeline {
    agent any

    stages {

        stage('Create web directory') {
            input {
                message 'Enter the data'
                parameters {
                    string(name:'AUTHOR', defaultValue: 'Sergio', description: 'Author of the deployment')
                    string(name:'ENVIRONMENT', defaultValue: 'Development', description: 'Environment to deploy')
                }
            }
            steps {
                echo "Responsible: ${AUTHOR} | Environment: ${ENVIRONMENT}"
                // Crear el directorio web dentro del home de Jenkins
                sh 'mkdir -p /var/jenkins_home/web'
                // Limpiar contenido anterior
                sh 'rm -rf /var/jenkins_home/web/*'
            }
        }

        stage('Copy web application') {
            steps {
                echo 'Copying web application...'
                sh 'cp -r web/* /var/jenkins_home/web/'
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
                  -v /var/jenkins_home/web:/usr/local/apache2/htdocs/ \
                  httpd
                '''
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
