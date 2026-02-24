Tú dijiste:
dede wsl2 :  docker run -d \
  --name jenkins \
  -u root ^
  -p 8484:8080 \
  -p 50000:50000 \
  -v ~/jenkins:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins
docker: invalid reference format

Run 'docker run --help' for more information
-p: command not found
nombre@EQUIPO:~$

ChatGPT Plus

El error viene de que estás en WSL2 (Linux/bash) pero estás usando el carácter ^, que es para PowerShell / CMD en Windows.

En Linux el carácter para continuar línea es \ (barra invertida), no ^.
✅ Comando correcto en WSL2

Ejecuta así:

docker run -d \
  --name jenkins \
  -u root \
  -p 8484:8080 \
  -p 50000:50000 \
  -v ~/jenkins:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts

🔎 Por qué te salió el error

    docker: invalid reference format
    → Porque el ^ cortó mal el comando y Docker interpretó mal la imagen.

    -p: command not found
    → Bash pensó que -p era un nuevo comando.

🚀 Alternativa (una sola línea)

También puedes correrlo todo en una sola línea:

docker run -d --name jenkins -u root -p 8484:8080 -p 50000:50000 -v ~/jenkins:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts

Si quieres, dime:

    ¿Estás usando Docker Desktop con WSL2?

    ¿Quieres que Jenkins pueda usar Docker dentro (Docker-in-Docker)?

Y te lo dejo configurado correctamente 🔥

Tú dijiste:
para configurar la url de jenkins en el inicio desde un contenedor me pone localhost y creo que es mejor poner la url del equipo, me muestra estas: ipconfig

Configuración IP de Windows


Adaptador de Ethernet Ethernet:

   Estado de los medios. . . . . . . . . . . : medios desconectados
   Sufijo DNS específico para la conexión. . : home

Adaptador de Ethernet vEthernet (Default Switch):

   Sufijo DNS específico para la conexión. . :
   Vínculo: dirección IPv6 local. . . : fe80::81ca:1747:f15d:9547%30
   Dirección IPv4. . . . . . . . . . . . . . : 172.19.112.1
   Máscara de subred . . . . . . . . . . . . : 255.255.240.0
   Puerta de enlace predeterminada . . . . . :

Adaptador de Ethernet vEthernet (conmutador virtual):

   Sufijo DNS específico para la conexión. . :
   Vínculo: dirección IPv6 local. . . : fe80::e939:3286:7ed6:ccc9%15
   Dirección IPv4. . . . . . . . . . . . . . : 192.168.0.13
   Máscara de subred . . . . . . . . . . . . : 255.255.255.0
   Puerta de enlace predeterminada . . . . . : 192.168.0.1

Adaptador de LAN inalámbrica Conexión de área local* 1:

   Estado de los medios. . . . . . . . . . . : medios desconectados
   Sufijo DNS específico para la conexión. . :

Adaptador de LAN inalámbrica Conexión de área local* 10:

   Estado de los medios. . . . . . . . . . . : medios desconectados
   Sufijo DNS específico para la conexión. . :

Adaptador de Ethernet VMware Network Adapter VMnet1:

   Sufijo DNS específico para la conexión. . :
   Vínculo: dirección IPv6 local. . . : fe80::bab0:fd8b:1b2a:986c%12
   Dirección IPv4. . . . . . . . . . . . . . : 192.168.116.1
   Máscara de subred . . . . . . . . . . . . : 255.255.255.0
   Puerta de enlace predeterminada . . . . . :

Adaptador de Ethernet VMware Network Adapter VMnet8:

   Sufijo DNS específico para la conexión. . :
   Vínculo: dirección IPv6 local. . . : fe80::c3b8:d6e7:84a:f560%21
   Dirección IPv4. . . . . . . . . . . . . . : 192.168.88.1
   Máscara de subred . . . . . . . . . . . . : 255.255.255.0
   Puerta de enlace predeterminada . . . . . :

Adaptador de Ethernet vEthernet (WSL):

   Sufijo DNS específico para la conexión. . :
   Vínculo: dirección IPv6 local. . . : fe80::a29b:40ad:68d0:e264%58
   Dirección IPv4. . . . . . . . . . . . . . : 172.30.32.1
   Máscara de subred . . . . . . . . . . . . : 255.255.240.0
   Puerta de enlace predeterminada . . . . . : no se cual debo indicar,pero el problema es que al reiniciar el equipo la ip suele cambiar, ¿no?, ¿como solucionarlo y cual poner?

ChatGPT Plus

Perfecto 👌 estás pensando correctamente.

Sí ❗ si dejas http://localhost:8484 en Jenkins solo funcionará desde tu propio equipo.
Si quieres acceder desde otro PC de tu red, debes usar la IP correcta de tu máquina.
✅ Qué IP debes usar

De todas las que muestras, la correcta es:

192.168.0.13

Porque:

    Es la red real de tu casa/oficina (192.168.0.x)

    Tiene puerta de enlace 192.168.0.1

    Es la que usa tu router

    No es virtual (VMware, WSL, etc.)

Entonces tu Jenkins quedaría:

http://192.168.0.13:8484

⚠️ El problema: la IP cambia al reiniciar

Correcto 👍 esa IP normalmente es dinámica (DHCP), así que puede cambiar.

Tienes 3 soluciones:
🥇 OPCIÓN RECOMENDADA: Reserva DHCP en el router

La mejor solución.

Entras al router (normalmente 192.168.0.1) y:

    Buscas DHCP Reservation o Reserva de IP

    Asignas la MAC de tu equipo

    Fijas siempre 192.168.0.13

✔ No vuelve a cambiar
✔ Es la solución profesional
✔ No rompe nada en Windows
🥈 Opción 2: IP fija en Windows

Configuras manualmente:

    IP: 192.168.0.50 (por ejemplo)

    Máscara: 255.255.255.0

    Puerta de enlace: 192.168.0.1

    DNS: 8.8.8.8

Funciona, pero si eliges una IP ya usada tendrás conflicto.
🥉 Opción 3 (MUY BUENA): usar nombre del equipo

En vez de IP, puedes usar:

http://NOMBRE-DEL-EQUIPO:8484

Prueba en otro PC:

http://EQUIPO:8484

Si funciona, es mejor que usar IP.

También puedes usar:

http://equipo.home:8484

(depende de tu red)
🔥 Configurar la URL dentro de Jenkins

Entra a:

Manage Jenkins
→ Configure System
→ Jenkins URL

Y pon:

http://192.168.0.13:8484

O mejor aún el nombre del equipo.
🧠 Importante (WSL2 + Docker)

Aunque Jenkins esté dentro de Docker en WSL2:

    Docker Desktop hace el port forwarding

    El acceso real siempre es por la IP de Windows

    NO debes usar la IP 172.x.x.x de WSL

🎯 Qué haría yo en tu caso

    Reservar IP en el router

    Configurar Jenkins con http://192.168.0.13:8484

    Listo, estable y limpio

Si quieres, dime:

    ¿Quieres acceder solo desde tu PC?

    ¿Desde otros PCs de tu red?

    ¿O desde internet?

Porque cambia bastante la configuración 😎

Tú dijiste:
voy a ejecutar esta pipeline desde git: pipeline {
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
                  -p 9000:80 \
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
                sh 'curl -f http://localhost:9000'
            }
        }
    }
}

ChatGPT Plus

Muy buena pipeline 👌 está bastante bien estructurada.
Te explico lo importante para que funcione correctamente en tu entorno WSL2 + Docker + Jenkins en contenedor.
🔎 1️⃣ Punto crítico: Docker dentro de Jenkins

Tú estás usando:

sh 'docker rm -f apache1 || true'

Eso solo funcionará si:

    Montaste /var/run/docker.sock

    Jenkins corre como root

Que ya habíamos dejado así cuando levantaste Jenkins con:

-v /var/run/docker.sock:/var/run/docker.sock
-u root

✔ Entonces Docker no es "Docker inside Docker",
✔ Es el Docker del host (Windows + WSL2).

Perfecto 👍
🔎 2️⃣ ¿Funcionará el volumen?

Aquí:

-v /var/jenkins_home/web:/usr/local/apache2/htdocs/

Esto funciona porque:

    /var/jenkins_home está dentro del contenedor Jenkins

    Pero también está mapeado a ~/jenkins en tu WSL

O sea:

WSL → carpeta real
Jenkins → ve esa carpeta
Apache → la monta

✔ Correcto.
⚠️ 3️⃣ Posible problema con web/*

En esta línea:

sh 'cp -r web/* /var/jenkins_home/web/'

Esto depende de que:

    Tu repo tenga una carpeta llamada web

    Jenkins esté ejecutándose en el workspace correcto

Para evitar errores más adelante, yo lo haría más seguro:

sh 'cp -r $WORKSPACE/web/* /var/jenkins_home/web/'

⚠️ 4️⃣ curl http://localhost:9000

Esto funciona porque:

    Jenkins está en el mismo host Docker

    El puerto 9000 está expuesto en el host

Pero si algún día ejecutas Jenkins en otro agente, podría fallar.

Más robusto sería:

sh 'curl -f http://host.docker.internal:9000'

(En Docker Desktop funciona mejor.)
🧠 5️⃣ Mejora profesional (esperar a Apache bien)

En vez de:

sh 'sleep 5'

Puedes hacer:

sh '''
for i in {1..10}; do
  curl -f http://localhost:9000 && break
  sleep 2
done
'''

Así espera hasta que Apache realmente esté listo.
🚀 6️⃣ Versión mejorada de tu pipeline

Te la dejo optimizada:

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
                sh 'mkdir -p /var/jenkins_home/web'
                sh 'rm -rf /var/jenkins_home/web/*'
            }
        }

        stage('Copy web application') {
            steps {
                echo 'Copying web application...'
                sh 'cp -r $WORKSPACE/web/* /var/jenkins_home/web/'
            }
        }

        stage('Recreate Apache container') {
            steps {
                echo 'Dropping and recreating Apache container...'
                sh 'docker rm -f apache1 || true'
                sh '''
                docker run -dit \
                  --name apache1 \
                  -p 9000:80 \
                  -v /var/jenkins_home/web:/usr/local/apache2/htdocs/ \
                  httpd
                '''
            }
        }

        stage('Check web app') {
            steps {
                echo 'Testing the web app...'
                sh '''
                for i in {1..10}; do
                  curl -f http://localhost:9000 && exit 0
                  sleep 2
                done
                exit 1
                '''
            }
        }
    }
}

🎯 Resultado final

Cuando termine la pipeline podrás acceder desde tu red en:

http://192.168.0.13:9000

(si esa es tu IP fija)

Si quieres, te puedo preparar la versión:

    🔹 Con docker-compose

    🔹 Con build de imagen propia

    🔹 Con pipeline multibranch desde Git

    🔹 Con versionado por tags

¿Cuál quieres montar ahora? 😎

Tú dijiste:
obtengo error: Started by user Administrador

Obtained Jenkinsfile from git https://github.com/jesus-p-s/WEB-Practice
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins
 in /var/jenkins_home/workspace/ejemplo1
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Declarative: Checkout SCM)
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
No credentials specified
Cloning the remote Git repository
Cloning repository https://github.com/jesus-p-s/WEB-Practice
 > git init /var/jenkins_home/workspace/ejemplo1 # timeout=10
Fetching upstream changes from https://github.com/jesus-p-s/WEB-Practice
 > git --version # timeout=10
 > git --version # 'git version 2.47.3'
 > git fetch --tags --force --progress -- https://github.com/jesus-p-s/WEB-Practice +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/jesus-p-s/WEB-Practice # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
Avoid second fetch
 > git rev-parse origin/main^{commit} # timeout=10
Checking out Revision 42e624ab6431dad9f451554781b753071e7987b5 (origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 42e624ab6431dad9f451554781b753071e7987b5 # timeout=10
Commit message: "Update Jenkinsfile"
First time build. Skipping changelog.
[Pipeline] }
[Pipeline] // stage
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Create web directory)
[Pipeline] input
Input requested
Approved by Administrador

[Pipeline] withEnv
[Pipeline] {
[Pipeline] echo
Responsible: Sergio | Environment: Development

[Pipeline] sh
+ mkdir -p /var/jenkins_home/web
[Pipeline] sh
+ rm -rf /var/jenkins_home/web/*
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Copy web application)
[Pipeline] echo
Copying web application...
[Pipeline] sh

+ cp -r web/buy.html web/clinic.html web/contact.html web/css web/images web/index.html web/js web/pet.html web/service.html /var/jenkins_home/web/
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Recreate Apache container)
[Pipeline] echo
Dropping and recreating Apache container...
[Pipeline] sh
+ docker rm -f apache1
/var/jenkins_home/workspace/ejemplo1@tmp/durable-34373af4/script.sh.copy: 1: docker: not found
+ true
[Pipeline] sh
+ docker run -dit --name apache1 -p 9000:80 -v /var/jenkins_home/web:/usr/local/apache2/htdocs/ httpd
/var/jenkins_home/workspace/ejemplo1@tmp/durable-da2cf968/script.sh.copy: 2: docker: not found
[Pipeline] }

[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Check web app)
Stage "Check web app" skipped due to earlier failure(s)
[Pipeline] getContext
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node
[Pipeline] End of Pipeline
ERROR: script returned exit code 127
Finished: FAILURE

ChatGPT Plus

Perfecto 👍 el log es clarísimo:

docker: not found

Eso significa que dentro del contenedor de Jenkins no está instalado el cliente Docker.

Aunque hayas montado:

-v /var/run/docker.sock:/var/run/docker.sock

👉 Eso solo conecta con el daemon
👉 Pero necesitas el binario docker dentro del contenedor Jenkins.
🔥 Solución correcta (la profesional)

Debes crear una imagen personalizada de Jenkins que tenga Docker CLI instalado.
🥇 PASO 1 — Crear Dockerfile

En WSL crea un directorio, por ejemplo:

mkdir jenkins-docker
cd jenkins-docker
nano Dockerfile

Pon esto:

FROM jenkins/jenkins:lts

USER root

RUN apt-get update && \
    apt-get install -y docker.io && \
    apt-get clean

USER jenkins

Guarda.
🥇 PASO 2 — Construir imagen

docker build -t jenkins-docker .

🥇 PASO 3 — Eliminar contenedor anterior

docker rm -f jenkins

🥇 PASO 4 — Levantar Jenkins con la nueva imagen

docker run -d \
  --name jenkins \
  -u root \
  -p 8484:8080 \
  -p 50000:50000 \
  -v ~/jenkins:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins-docker

🧪 Verificar

Entra al contenedor:

docker exec -it jenkins bash
docker --version

Si muestra versión → listo ✅
🚀 Después de esto

Tu pipeline funcionará correctamente:

sh 'docker rm -f apache1 || true'
sh 'docker run -dit ...'

Y sí se creará el contenedor Apache (httpd).
🧠 Por qué pasa esto

Hay 2 cosas distintas:

    🔌 Socket Docker → conecta con el daemon

    🛠️ Cliente Docker → ejecuta el comando docker

Tú solo tenías el 1.
🎯 Alternativa más avanzada (cuando quieras)

Más adelante puedes hacerlo mejor usando:

    Agente Docker

    Docker Pipeline plugin

    docker.build()

    docker.withRegistry()

Pero primero hagámoslo funcionar básico 💪

Cuando lo levantes de nuevo dime qué sale en:

docker ps

Y lo dejamos perfecto 😎

Tú dijiste:
este dockerfile no instalar dind ? : FROM jenkins/jenkins:lts
USER root
RUN apt-get update && apt-get install -y lsb-release ca-certificates curl && \
    install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc && \
    chmod a+r /etc/apt/keyrings/docker.asc && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] \
    https://download.docker.com/linux/debian $(. /etc/os-release && echo \"$VERSION_CODENAME\") stable" \
    | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && apt-get install -y docker-ce-cli docker-compose-plugin && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

USER jenkins

# Add Jenkins plugins (pinned versions to avoid missing deps at runtime)
COPY --chown=jenkins:jenkins plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt --latest false

ChatGPT Plus

Muy buena pregunta 👌
No, ese Dockerfile NO instala Docker-in-Docker (DinD).

Instala solo el cliente de Docker, no el daemon.
🔎 Qué está instalando realmente

Esta línea:

apt-get install -y docker-ce-cli docker-compose-plugin

Instala:

    ✅ docker (CLI)

    ✅ docker compose

    ❌ NO instala dockerd

    ❌ NO instala el servicio Docker

O sea:

👉 Es Docker CLI only
👉 Necesita conectarse a un Docker daemon externo
👉 En tu caso: al Docker del host mediante:

-v /var/run/docker.sock:/var/run/docker.sock

Y eso es EXACTAMENTE lo que tú quieres.
🧠 Entonces… ¿qué es Docker-in-Docker (DinD)?

DinD sería esto:

apt-get install docker-ce

y luego arrancar dockerd dentro del contenedor.

Eso implica:

    Contenedor privilegiado (--privileged)

    Más consumo

    Más complejidad

    Más problemas de seguridad

🎯 Tu caso (WSL2 + Docker Desktop)

La arquitectura correcta es:

Windows
 └── Docker Desktop (daemon real)
      └── Jenkins container
            └── docker CLI
                  └── usa /var/run/docker.sock

✔ Es más limpio
✔ Es más rápido
✔ Es la práctica recomendada
🔥 Resumen claro

Tu Dockerfile:
Componente	¿Instalado?
docker CLI	✅
docker compose	✅
docker daemon	❌
Docker-in-Docker	❌

Y eso está PERFECTO para tu pipeline.
🧪 Cómo verificar

Después de levantar Jenkins con esa imagen:

docker exec -it jenkins bash
docker version

Si ves:

Client: Docker Engine
Server: Docker Engine

→ entonces está usando correctamente el daemon del host.
💡 Conclusión

Tu Dockerfile es:

✔ Profesional
✔ Correcto
✔ Mejor que instalar docker.io
✔ No es DinD
✔ Es la arquitectura recomendada

Si quieres, ahora podemos mejorar tu pipeline para que use:

    docker compose

    o docker.build()

    o versionado automático

¿Qué nivel quieres montar ahora? 😎

Tú dijiste:
C:\Docker>docker exec -it jenkins bash
docker versionroot@a99cd8650aaf:/# docker version
bash: docker: command not found
root@a99cd8650aaf:/#

ChatGPT Plus

Perfecto 👌 esto confirma algo importante:

👉 Esa imagen que está corriendo NO es la que tiene docker-ce-cli instalado.

Porque dentro del contenedor:

docker: command not found

Eso significa que Jenkins sigue usando:

jenkins/jenkins:lts

y NO la imagen personalizada que construiste.
🔎 Vamos a comprobarlo

En tu Windows ejecuta:

docker ps

Mira la columna IMAGE del contenedor jenkins.

Seguramente verás algo como:

jenkins/jenkins:lts

Si es así → estás arrancando el contenedor viejo.
✅ SOLUCIÓN CORRECTA
1️⃣ Verifica que tu imagen existe

docker images

Deberías ver algo como:

jenkins-docker   latest

(si ese fue el nombre que usaste en docker build -t jenkins-docker .)
2️⃣ Borra el contenedor actual

docker rm -f jenkins

3️⃣ Levántalo usando TU imagen

⚠️ Este paso es el que normalmente se olvida:

docker run -d \
  --name jenkins \
  -u root \
  -p 8484:8080 \
  -p 50000:50000 \
  -v ~/jenkins:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins-docker

🔴 Fíjate que la última línea debe ser:

jenkins-docker

NO jenkins/jenkins:lts
4️⃣ Verificar otra vez

docker exec -it jenkins bash
docker version

Ahora debería mostrar cliente y server.
🧠 Por qué pasó esto

Construiste bien la imagen ✔
Pero arrancaste el contenedor con la imagen oficial ❌

Docker no reemplaza automáticamente el contenedor anterior.
🎯 Cuando lo tengas funcionando

Tu pipeline:

sh 'docker rm -f apache1 || true'
sh 'docker run -dit ...'

Va a funcionar sin el error docker: not found.

Si quieres, mándame el resultado de:

docker images
docker ps

Y lo revisamos en 10 segundos 😎

Tú dijiste:
C:\Docker>docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                                                                                          NAMES
a99cd8650aaf   jenkins/jenkins:lts   "/usr/bin/tini -- /u…"   13 minutes ago   Up 13 minutes   0.0.0.0:50000->50000/tcp, [::]:50000->50000/tcp, 0.0.0.0:8484->8080/tcp, [::]:8484->8080/tcp   jenkins

ChatGPT Plus

Ahí está el problema 👇

IMAGE
jenkins/jenkins:lts

Estás ejecutando la imagen oficial de Jenkins,
no tu imagen personalizada con Docker CLI.

Por eso dentro del contenedor aparece:

docker: command not found

🔥 Haz esto exactamente
1️⃣ Verifica que tu imagen personalizada existe

docker images

Deberías ver algo como:

jenkins-docker   latest

Si NO aparece → no se construyó correctamente.
2️⃣ Elimina el contenedor actual

docker rm -f jenkins

3️⃣ Arráncalo con TU imagen (este es el paso clave)

Si tu imagen se llama jenkins-docker:

docker run -d ^
  --name jenkins ^
  -u root ^
  -p 8484:8080 ^
  -p 50000:50000 ^
  -v C:\Docker\jenkins:/var/jenkins_home ^
  -v /var/run/docker.sock:/var/run/docker.sock ^
  jenkins-docker

⚠️ IMPORTANTE:

    En PowerShell usa ^

    En WSL usa \

    La última línea debe ser jenkins-docker, NO jenkins/jenkins:lts

4️⃣ Verifica

docker exec -it jenkins bash
docker version

Debe mostrar:

Client: Docker Engine
Server: Docker Engine

🧠 Lo que pasó

Construiste la imagen personalizada ✔
Pero levantaste el contenedor con la imagen oficial ❌

Docker no reemplaza automáticamente contenedores existentes.

Cuando lo levantes bien, tu pipeline dejará de fallar en:

docker rm -f apache1

y ya creará el contenedor httpd sin error 🚀

Si quieres, pásame ahora el resultado de:

docker images

y confirmamos que tu imagen está lista.

Tú dijiste:
Started by user Administrador

Obtained Jenkinsfile from git https://github.com/jesus-p-s/WEB-Practice
[Pipeline] Start of Pipeline
[Pipeline] node
Running on Jenkins
 in /var/jenkins_home/workspace/ejemplo1
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Declarative: Checkout SCM)
[Pipeline] checkout
Selected Git installation does not exist. Using Default
The recommended git tool is: NONE
No credentials specified
 > git rev-parse --resolve-git-dir /var/jenkins_home/workspace/ejemplo1/.git # timeout=10
Fetching changes from the remote Git repository
 > git config remote.origin.url https://github.com/jesus-p-s/WEB-Practice # timeout=10
Fetching upstream changes from https://github.com/jesus-p-s/WEB-Practice
 > git --version # timeout=10
 > git --version # 'git version 2.47.3'
 > git fetch --tags --force --progress -- https://github.com/jesus-p-s/WEB-Practice +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git rev-parse origin/main^{commit} # timeout=10
Checking out Revision 42e624ab6431dad9f451554781b753071e7987b5 (origin/main)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 42e624ab6431dad9f451554781b753071e7987b5 # timeout=10
Commit message: "Update Jenkinsfile"
 > git rev-list --no-walk 42e624ab6431dad9f451554781b753071e7987b5 # timeout=10
[Pipeline] }
[Pipeline] // stage
[Pipeline] withEnv
[Pipeline] {
[Pipeline] stage
[Pipeline] { (Create web directory)
[Pipeline] input
Input requested
Approved by Administrador

[Pipeline] withEnv
[Pipeline] {
[Pipeline] echo
Responsible: Sergio | Environment: Development
[Pipeline] sh

+ mkdir -p /var/jenkins_home/web
[Pipeline] sh
+ rm -rf /var/jenkins_home/web/buy.html /var/jenkins_home/web/clinic.html /var/jenkins_home/web/contact.html /var/jenkins_home/web/css /var/jenkins_home/web/images /var/jenkins_home/web/index.html /var/jenkins_home/web/js /var/jenkins_home/web/pet.html /var/jenkins_home/web/service.html
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Copy web application)
[Pipeline] echo
Copying web application...
[Pipeline] sh

+ cp -r web/buy.html web/clinic.html web/contact.html web/css web/images web/index.html web/js web/pet.html web/service.html /var/jenkins_home/web/
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Recreate Apache container)
[Pipeline] echo
Dropping and recreating Apache container...
[Pipeline] sh
+ docker rm -f apache1
Error response from daemon: No such container: apache1
[Pipeline] sh
+ docker run -dit --name apache1 -p 9000:80 -v /var/jenkins_home/web:/usr/local/apache2/htdocs/ httpd
Unable to find image 'httpd:latest' locally

latest: Pulling from library/httpd
0c8d55a45c0d: Pulling fs layer
fe1db8dd446f: Pulling fs layer
4f4fb700ef54: Pulling fs layer
30973b009bab: Pulling fs layer
85b0d820aa56: Pulling fs layer
996228ca33ab: Pulling fs layer
85b0d820aa56: Waiting
996228ca33ab: Waiting
30973b009bab: Waiting
4f4fb700ef54: Download complete
fe1db8dd446f: Verifying Checksum
fe1db8dd446f: Download complete

30973b009bab: Download complete

996228ca33ab: Verifying Checksum
996228ca33ab: Download complete
85b0d820aa56: Verifying Checksum
85b0d820aa56: Download complete
0c8d55a45c0d: Download complete

0c8d55a45c0d: Pull complete
fe1db8dd446f: Pull complete
4f4fb700ef54: Pull complete
30973b009bab: Pull complete

85b0d820aa56: Pull complete
996228ca33ab: Pull complete
Digest: sha256:b89c19a390514d6767e8c62f29375d0577190be448f63b24f5f11d6b03f7bf18
Status: Downloaded newer image for httpd:latest
678ac645168f537bdeb634dda3a4340b10dc0fd5282b7083485fe180ccc59576
[Pipeline] }
[Pipeline] // stage
[Pipeline] stage
[Pipeline] { (Check web app)
[Pipeline] echo
Testing the web app...
[Pipeline] sh

+ sleep 5

[Pipeline] sh
+ curl -f http://localhost:9000
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed

  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
curl: (7) Failed to connect to localhost port 9000 after 0 ms: Could not connect to server
[Pipeline] }
[Pipeline] // stage
[Pipeline] }
[Pipeline] // withEnv
[Pipeline] }
[Pipeline] // node

[Pipeline] End of Pipeline
ERROR: script returned exit code 7
Finished: FAILURE

ChatGPT Plus

Perfecto 👌 ahora Docker sí funciona, el contenedor httpd se crea correctamente ✅

El problema ahora es este:

curl: (7) Failed to connect to localhost port 9000

Y esto es completamente normal en tu arquitectura.
🎯 ¿Qué está pasando?

Tu pipeline corre dentro del contenedor de Jenkins.

Cuando haces:

curl http://localhost:9000

localhost dentro del contenedor Jenkins significa:

👉 el propio contenedor Jenkins
NO el host
NO el contenedor Apache
🧠 Arquitectura real ahora mismo

Windows
 └── Docker Desktop (daemon)
      ├── Jenkins container
      └── apache1 container

El puerto 9000 está expuesto en el host, no dentro del contenedor Jenkins.

Por eso localhost:9000 falla.
✅ SOLUCIÓN CORRECTA

En Docker Desktop (Windows + WSL2), debes usar:

host.docker.internal

Cambia tu stage final a:

stage('Check web app') {
    steps {
        echo 'Testing the web app...'
        sh 'sleep 5'
        sh 'curl -f http://host.docker.internal:9000'
    }
}

🔥 ¿Por qué funciona eso?

host.docker.internal es un DNS especial que Docker Desktop crea para que los contenedores puedan acceder al host.

Entonces:

Jenkins container → host.docker.internal → Windows host → puerto 9000 → apache1

🚀 Alternativa más profesional (mejor aún)

En vez de usar el puerto publicado, puedes conectar los contenedores por red Docker.

Por ejemplo:

docker network create jenkins-net

Levantar Jenkins y Apache con:

--network jenkins-net

Y luego desde Jenkins hacer:

curl http://apache1

Pero eso ya es nivel siguiente 😎
🎯 Qué debes hacer ahora

    Cambia localhost por:

http://host.docker.internal:9000

    Ejecuta de nuevo la pipeline

Debería terminar en SUCCESS ✅

Si después de cambiarlo sigue fallando, pásame el nuevo log y lo afinamos.
Ya estás en la parte interesante 🔥

Tú dijiste:
en jenkins aparece : Parece que la configuración de proxy inverso está mal

ChatGPT Plus

Perfecto 👌 ahora estamos en otro tema distinto.

El mensaje:

    "Parece que la configuración de proxy inverso está mal"

lo muestra Jenkins cuando la URL configurada en Jenkins no coincide con cómo estás accediendo realmente.

No es un error crítico, pero conviene arreglarlo.
🎯 Por qué aparece

Jenkins compara:

    🔹 La URL configurada en:

    Manage Jenkins → Configure System → Jenkins URL

    🔹 La URL real con la que estás entrando al navegador

Si no coinciden → muestra advertencia de proxy inverso.
🔎 En tu caso seguramente pasa esto:

Configuraste algo como:

http://192.168.0.13:8484

Pero estás entrando con:

http://localhost:8484

O al revés.

Entonces Jenkins detecta que el Host header no coincide.
✅ SOLUCIÓN SIMPLE (la correcta para tu caso)

Si SOLO accedes desde tu PC:

    Ve a:

    Manage Jenkins
    → Configure System
    → Jenkins URL

    Pon exactamente:

http://localhost:8484/

(Con la barra final)

    Guarda

    Refresca la página

Listo ✅
🧠 Si accedes desde otros PCs

Entonces debes poner:

http://192.168.0.13:8484/

Y siempre entrar usando esa IP, nunca localhost.
🚫 Esto NO es un error de Docker

No tiene nada que ver con:

    WSL

    Apache

    Tu pipeline

    Docker socket

Es solo una validación interna de Jenkins.
🔥 Cuándo es realmente importante

Solo importa si:

    Usas Nginx o Apache como reverse proxy

    Usas HTTPS

    Usas autenticación externa

    Usas webhooks

    Usas GitHub OAuth

En tu laboratorio actual, puedes ignorarlo sin problema.
🎯 Recomendación final

Para entorno local de prácticas:

✔ Configura Jenkins URL como:

http://localhost:8484/

✔ Accede siempre igual

Y desaparece la advertencia.

Si quieres, dime exactamente con qué URL entras tú al navegador y te digo cuál debes configurar 😎

Tú dijiste:
tambien tengo: Building on the built-in node can be a security issue. You should set up distributed builds. See the documentation. 

ChatGPT Plus

Perfecto 👌 ahora estás viendo advertencias “buenas” de Jenkins 😄

El mensaje:

    “Building on the built-in node can be a security issue…”

NO es un error.
Es una recomendación de seguridad.
🎯 ¿Qué significa?

Tu pipeline está ejecutándose en:

Running on Jenkins

Eso es el nodo built-in (antes llamado master).

Jenkins recomienda:

    ❌ No ejecutar builds en el nodo principal

    ✅ Usar agentes (nodos secundarios)

Porque el nodo principal:

    Maneja credenciales

    Maneja configuración

    Maneja plugins

    Es el cerebro del sistema

Si un build malicioso corre ahí → puede comprometer todo.
🧠 En tu caso (laboratorio local)

Estás:

    En entorno local

    Sin usuarios externos

    Sin credenciales críticas

    Haciendo pruebas

👉 Puedes ignorarlo completamente.

No afecta en nada.
🥇 Si quisieras hacerlo “correcto” (modo profesional)

Hay 2 formas:
Opción A — Deshabilitar builds en el built-in node

    Ve a:

    Manage Jenkins
    → Nodes
    → Built-In Node

    Añade un label vacío o marca que no acepte builds.

Luego creas un agente Docker.
Opción B — Usar agente Docker en la pipeline

Por ejemplo:

pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

Eso hace que cada build corra en un contenedor limpio.
🧩 En empresas reales se hace así:

Jenkins Controller (solo coordina)
       ↓
Agentes (Docker, Kubernetes, VM, etc.)

Controller = cerebro
Agentes = workers
🚦 ¿Qué te recomiendo?

Para tu entorno actual:

👉 Ignóralo
👉 No afecta nada
👉 No tiene relación con tu error anterior
🎓 Pero ojo…

Si en algún momento:

    Abres Jenkins a internet

    Añades más usuarios

    Usas credenciales reales

    Usas GitHub Webhooks

Entonces sí deberías separar controller y agentes.

Si quieres, puedo explicarte en 5 minutos cómo convertir tu laboratorio en arquitectura profesional tipo DevOps real 😎

Tú dijiste:
Advertencias publicadas para los siguientes componentes instalados:

HTML Publisher plugin 1.36
    File path information disclosure
    A fix for this issue is available. Go to the plugin manager to update the plugin.

ChatGPT Plus

Perfecto 👌 ahora estamos viendo advertencias de seguridad de plugins en Jenkins.

El mensaje dice:

    HTML Publisher plugin 1.36 – File path information disclosure

🎯 Qué significa

    El plugin HTML Publisher 1.36 tiene un problema de seguridad:
    puede exponer información de rutas de archivos del sistema del servidor Jenkins.

    Esto NO compromete tu pipeline directamente, pero si Jenkins estuviera expuesto a internet, un atacante podría obtener información sensible sobre la estructura de tu servidor.

✅ Solución recomendada

    Ve a:

Manage Jenkins → Manage Plugins → Updates

    Busca HTML Publisher

    Actualiza a la última versión disponible

    Reinicia Jenkins si lo solicita

🧠 Nota importante

    Si estás en laboratorio local, sin acceso externo → riesgo prácticamente nulo

    Es buena práctica mantener plugins actualizados para evitar problemas cuando crezcas

    Jenkins te avisa cada vez que detecta vulnerabilidades conocidas

⚡ Extra tip

Para ver todas las vulnerabilidades conocidas:

Manage Jenkins → Manage Plugins → Installed → Check for Updates

Ahí verás si algún plugin más necesita actualización.

Si quieres, puedo hacer una mini-guía para actualizar TODOS los plugins críticos de tu Jenkins de laboratorio, evitando estas advertencias de seguridad 😎

¿Quieres que haga eso?

Tú dijiste:
Jenkins can enforce Content Security Policy (CSP). CSP tells web browsers what they are allowed to do while rendering a web page. This limits or even eliminates the impact of vulnerabilities like cross-site scripting (XSS). CSP is disabled by default for backward compatibility, but it is recommended to enable it, if possible. 

ChatGPT Plus

Exacto 👌 estás viendo la advertencia sobre Content Security Policy (CSP) en Jenkins.

Te explico con detalle:
🔎 Qué es CSP

CSP (Content Security Policy) es un mecanismo de seguridad web que:

    Le dice al navegador qué recursos puede cargar (JS, CSS, imágenes, etc.).

    Limita o elimina vulnerabilidades como:

        XSS (cross-site scripting)

        Inclusión de contenido malicioso

        Carga de scripts externos no autorizados

🎯 Por qué Jenkins lo muestra

    Por compatibilidad con plugins antiguos, Jenkins tiene CSP desactivado por defecto.

    Si lo activas, algunos plugins muy antiguos podrían romper la interfaz o mostrar errores.

    La advertencia es informativa, no significa que tu Jenkins esté comprometido.

✅ Cómo activarlo (recomendado)

    Ve a:

Manage Jenkins → Configure Global Security

    Busca sección Markup Formatter / Content Security Policy

    Activa CSP y selecciona la política por defecto (o una personalizada si sabes lo que haces)

    Guarda y reinicia Jenkins si es necesario

⚠️ Posibles efectos

    Algunos plugins antiguos pueden dejar de funcionar correctamente en la UI.

    Puede requerir ajustar “CSP rules” si ves errores de scripts bloqueados.

    En laboratorios locales esto no es crítico, pero en producción sí es recomendable.

💡 Recomendación práctica

    Para laboratorio o prácticas: puedes dejarlo desactivado sin problema.

    Para producción o exposición a internet: activa CSP y ajusta reglas si algún plugin falla.

Si quieres, puedo escribirte una configuración segura de CSP lista para Jenkins, que evita XSS sin romper la mayoría de plugins 🔐.

¿Quieres que lo haga?

Tú dijiste:
en Markup Formatter / muestra un desplegable con PLain Text (seleccionado) y safe HTML

ChatGPT Plus

¡Ah, perfecto! Eso es un poco diferente de lo que hablamos de CSP. Te explico la diferencia y qué hacer:
🔎 Markup Formatter en Jenkins

En:

Manage Jenkins → Configure Global Security → Markup Formatter

Ves un desplegable con dos opciones:

    Plain Text (seleccionado por defecto)

        Todo el contenido HTML que pongas se trata como texto plano.

        Nada se renderiza como HTML.

        Muy seguro, pero si un plugin genera reportes en HTML, no se verá bien.

    Safe HTML

        Permite que Jenkins renderice HTML limitado y seguro.

        Usa un filtro de etiquetas permitidas.

        Evita inyecciones XSS y la mayoría de ataques de scripts.

🔑 Relación con CSP

    Markup Formatter = qué HTML se permite dentro de Jenkins

    CSP = reglas del navegador sobre qué scripts y recursos externos se pueden ejecutar

Activar Safe HTML no activa CSP, pero sí reduce riesgo de XSS dentro de Jenkins.
✅ Recomendación

Para laboratorios:

    Mantén Plain Text si no necesitas mostrar reportes HTML.

    Cambia a Safe HTML si quieres que dashboards y reportes de plugins (como HTML Publisher) se vean correctamente.

Para producción:

    Safe HTML + activar CSP es lo más seguro.

Si quieres, puedo decirte exactamente cómo configurar Safe HTML + CSP para que tus pipelines y plugins sigan funcionando y quede seguro 🔐

Tú dijiste:
tengo este contenedor con una aplicacion web : {
	"Id": "65d56e9aeed15e3d13e6aafdc0f843e8da274a8cf0dd526217a25d3a0448214b",
	"Created": "2026-02-24T14:01:37.591132149Z",
	"Path": "httpd-foreground",
	"Args": [],
	"State": {
		"Status": "running",
		"Running": true,
		"Paused": false,
		"Restarting": false,
		"OOMKilled": false,
		"Dead": false,
		"Pid": 5895,
		"ExitCode": 0,
		"Error": "",
		"StartedAt": "2026-02-24T14:01:37.736331275Z",
		"FinishedAt": "0001-01-01T00:00:00Z"
	},
	"Image": "sha256:d2825031e94c68c5437ae2f479a1e2e1b2e0a26990c506e17deee19590546735",
	"ResolvConfPath": "/var/lib/docker/containers/65d56e9aeed15e3d13e6aafdc0f843e8da274a8cf0dd526217a25d3a0448214b/resolv.conf",
	"HostnamePath": "/var/lib/docker/containers/65d56e9aeed15e3d13e6aafdc0f843e8da274a8cf0dd526217a25d3a0448214b/hostname",
	"HostsPath": "/var/lib/docker/containers/65d56e9aeed15e3d13e6aafdc0f843e8da274a8cf0dd526217a25d3a0448214b/hosts",
	"LogPath": "/var/lib/docker/containers/65d56e9aeed15e3d13e6aafdc0f843e8da274a8cf0dd526217a25d3a0448214b/65d56e9aeed15e3d13e6aafdc0f843e8da274a8cf0dd526217a25d3a0448214b-json.log",
	"Name": "/apache1",
	"RestartCount": 0,
	"Driver": "overlay2",
	"Platform": "linux",
	"MountLabel": "",
	"ProcessLabel": "",
	"AppArmorProfile": "",
	"ExecIDs": null,
	"HostConfig": {
		"Binds": [
			"/var/jenkins_home/web:/usr/local/apache2/htdocs/"
		],
		"ContainerIDFile": "",
		"LogConfig": {
			"Type": "json-file",
			"Config": {}
		},
		"NetworkMode": "bridge",
		"PortBindings": {
			"80/tcp": [
				{
					"HostIp": "",
					"HostPort": "9001"
				}
			]
		},
		"RestartPolicy": {
			"Name": "no",
			"MaximumRetryCount": 0
		},
		"AutoRemove": false,
		"VolumeDriver": "",
		"VolumesFrom": null,
		"ConsoleSize": [
			0,
			0
		],
		"CapAdd": null,
		"CapDrop": null,
		"CgroupnsMode": "private",
		"Dns": null,
		"DnsOptions": [],
		"DnsSearch": [],
		"ExtraHosts": null,
		"GroupAdd": null,
		"IpcMode": "private",
		"Cgroup": "",
		"Links": null,
		"OomScoreAdj": 0,
		"PidMode": "",
		"Privileged": false,
		"PublishAllPorts": false,
		"ReadonlyRootfs": false,
		"SecurityOpt": null,
		"UTSMode": "",
		"UsernsMode": "",
		"ShmSize": 67108864,
		"Runtime": "runc",
		"Isolation": "",
		"CpuShares": 0,
		"Memory": 0,
		"NanoCpus": 0,
		"CgroupParent": "",
		"BlkioWeight": 0,
		"BlkioWeightDevice": [],
		"BlkioDeviceReadBps": [],
		"BlkioDeviceWriteBps": [],
		"BlkioDeviceReadIOps": [],
		"BlkioDeviceWriteIOps": [],
		"CpuPeriod": 0,
		"CpuQuota": 0,
		"CpuRealtimePeriod": 0,
		"CpuRealtimeRuntime": 0,
		"CpusetCpus": "",
		"CpusetMems": "",
		"Devices": [],
		"DeviceCgroupRules": null,
		"DeviceRequests": null,
		"MemoryReservation": 0,
		"MemorySwap": 0,
		"MemorySwappiness": null,
		"OomKillDisable": null,
		"PidsLimit": null,
		"Ulimits": [],
		"CpuCount": 0,
		"CpuPercent": 0,
		"IOMaximumIOps": 0,
		"IOMaximumBandwidth": 0,
		"MaskedPaths": [
			"/proc/acpi",
			"/proc/asound",
			"/proc/interrupts",
			"/proc/kcore",
			"/proc/keys",
			"/proc/latency_stats",
			"/proc/sched_debug",
			"/proc/scsi",
			"/proc/timer_list",
			"/proc/timer_stats",
			"/sys/devices/virtual/powercap",
			"/sys/firmware"
		],
		"ReadonlyPaths": [
			"/proc/bus",
			"/proc/fs",
			"/proc/irq",
			"/proc/sys",
			"/proc/sysrq-trigger"
		]
	},
	"GraphDriver": {
		"Data": {
			"ID": "65d56e9aeed15e3d13e6aafdc0f843e8da274a8cf0dd526217a25d3a0448214b",
			"LowerDir": "/var/lib/docker/overlay2/9a149a4a01a5ef87589811f57e9b90e4144f7b78bf7a11d73f31db31013e5b14-init/diff:/var/lib/docker/overlay2/ea668637955e8854dc20c18fd3c0e7a259e718ae02a68e715fe67a59bec16c04/diff:/var/lib/docker/overlay2/ed19f16dd710601ddddeb50d14473b1db6bbb6dc9ae0dd9d936d149f936051d8/diff:/var/lib/docker/overlay2/08889afbbcdf67fd8dd7dee59e8cbe425a83db02d6aca07bb83bcb213ade4bf8/diff:/var/lib/docker/overlay2/98a534551db9e26b1023ce11f32f332b477c3b8fb794378135af091743e522c0/diff:/var/lib/docker/overlay2/585c7afb5480059799b5097bb79772355ac8070effb1590495b25a391e3680bf/diff:/var/lib/docker/overlay2/573da04224598d7bf7e99b605f1fc63b9423af11d41404929fd53cf8f26b803a/diff",
			"MergedDir": "/var/lib/docker/overlay2/9a149a4a01a5ef87589811f57e9b90e4144f7b78bf7a11d73f31db31013e5b14/merged",
			"UpperDir": "/var/lib/docker/overlay2/9a149a4a01a5ef87589811f57e9b90e4144f7b78bf7a11d73f31db31013e5b14/diff",
			"WorkDir": "/var/lib/docker/overlay2/9a149a4a01a5ef87589811f57e9b90e4144f7b78bf7a11d73f31db31013e5b14/work"
		},
		"Name": "overlay2"
	},
	"Mounts": [
		{
			"Type": "bind",
			"Source": "/run/desktop/mnt/host/wsl/docker-desktop-bind-mounts/Ubuntu-22.04/39d1be74a6c2067daff4e9d3be67615fe547948e0bf7bebce1dbd5a80b35f104",
			"Destination": "/usr/local/apache2/htdocs",
			"Mode": "",
			"RW": true,
			"Propagation": "rprivate"
		}
	],
	"Config": {
		"Hostname": "65d56e9aeed1",
		"Domainname": "",
		"User": "",
		"AttachStdin": false,
		"AttachStdout": false,
		"AttachStderr": false,
		"ExposedPorts": {
			"80/tcp": {}
		},
		"Tty": true,
		"OpenStdin": true,
		"StdinOnce": false,
		"Env": [
			"PATH=/usr/local/apache2/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
			"HTTPD_PREFIX=/usr/local/apache2",
			"HTTPD_VERSION=2.4.66",
			"HTTPD_SHA256=94d7ff2b42acbb828e870ba29e4cbad48e558a79c623ad3596e4116efcfea25a",
			"HTTPD_PATCHES="
		],
		"Cmd": [
			"httpd-foreground"
		],
		"Image": "httpd",
		"Volumes": null,
		"WorkingDir": "/usr/local/apache2",
		"Entrypoint": null,
		"Labels": {
			"desktop.docker.io/wsl-distro": "Ubuntu-22.04"
		},
		"StopSignal": "SIGWINCH",
		"StopTimeout": 1
	},
	"NetworkSettings": {
		"SandboxID": "2fdfa7cd5e881c08f12f956f3d41db986e0420fd4074ce08f49d7200773ea5dd",
		"SandboxKey": "/var/run/docker/netns/2fdfa7cd5e88",
		"Ports": {
			"80/tcp": [
				{
					"HostIp": "0.0.0.0",
					"HostPort": "9001"
				},
				{
					"HostIp": "::",
					"HostPort": "9001"
				}
			]
		},
		"Networks": {
			"bridge": {
				"IPAMConfig": null,
				"Links": null,
				"Aliases": null,
				"DriverOpts": null,
				"GwPriority": 0,
				"NetworkID": "2248c279df330e44425bf4d58fb1e41371990754d3ea237705b416c43c925b81",
				"EndpointID": "114559c1e1c4651fc133ec29e445c4e855c85011b4422bbe0abdf48fc6e0b092",
				"Gateway": "172.17.0.1",
				"IPAddress": "172.17.0.3",
				"MacAddress": "0a:03:ef:7e:ce:f7",
				"IPPrefixLen": 16,
				"IPv6Gateway": "",
				"GlobalIPv6Address": "",
				"GlobalIPv6PrefixLen": 0,
				"DNSNames": null
			}
		}
	}
}

ChatGPT Plus

Perfecto, gracias por compartir toda la información del contenedor. Con esto podemos analizar exactamente cómo acceder a tu aplicación web y cómo integrarla con Jenkins correctamente.
🔎 Resumen del contenedor apache1

    Estado: corriendo (Running: true)

    Imagen: httpd

    Puerto expuesto: 80/tcp dentro del contenedor → mapeado al host en el puerto 9001

"Ports": {
  "80/tcp": [
    { "HostIp": "0.0.0.0", "HostPort": "9001" },
    { "HostIp": "::", "HostPort": "9001" }
  ]
}

    Volumen:
    Contiene tu aplicación web mapeada desde:

"/var/jenkins_home/web" → "/usr/local/apache2/htdocs"

    Red: usa la red bridge de Docker, con IP interna 172.17.0.3.

🎯 Cómo acceder desde Jenkins
Problema anterior:

    Tu pipeline intentaba hacer:

curl http://localhost:9000

    Esto fallaba porque:

        Jenkins corre dentro de un contenedor

        Apache está en otro contenedor

        Puerto 9001 está publicado en el host, no dentro del contenedor Jenkins

Solución inmediata:

Dentro de tu pipeline, cambia la URL a:

curl http://host.docker.internal:9001

Explicación:

    host.docker.internal apunta al host Windows desde dentro de cualquier contenedor

    9001 es el puerto que mapeaste al host

    Esto permitirá que Jenkins consulte correctamente el Apache

🔹 Alternativa más “profesional”

Si quieres evitar host.docker.internal, puedes conectar ambos contenedores en la misma red de Docker:

docker network create jenkins-net
docker network connect jenkins-net jenkins
docker network connect jenkins-net apache1

Luego puedes usar dentro del contenedor Jenkins:

curl http://apache1:80

    apache1 es el nombre del contenedor

    :80 es el puerto interno del contenedor Apache

Esto evita depender de puertos host, más seguro y estable.
🔹 Pipeline corregida (solo etapa de check web app)

stage('Check web app') {
    steps {
        echo 'Testing the web app...'
        sh 'sleep 5'
        sh 'curl -f http://host.docker.internal:9001'
    }
}

    Esto debería funcionar de inmediato en tu setup actual.

Si quieres, puedo escribirte una versión completa de tu pipeline que:

    Cree /var/jenkins_home/web

    Copie la app

    Levante el contenedor Apache

    Testee la web
    ✅ usando host.docker.internal o la red Docker interna para que sea totalmente confiable.

¿Quieres que haga eso?

Tú dijiste:
pero si accedo como http://localhost:9001/ o con http://host.docker.internal:9001/ no me meustra la web, solo Index of /

ChatGPT Plus

Ah, perfecto, ahora entiendo exactamente lo que pasa 😎

Cuando ves “Index of /” en lugar de tu aplicación, significa que Apache está funcionando y sirve la raíz, pero no encuentra tus archivos web en la ruta esperada.

Vamos a analizarlo paso a paso.
🔎 Qué está pasando

    Tu contenedor Apache tiene esto:

/usr/local/apache2/htdocs/ → DocumentRoot

    Está montando este volumen desde Jenkins:

/var/jenkins_home/web → /usr/local/apache2/htdocs

    Dentro de Jenkins, tu pipeline hace:

cp -r web/* /var/jenkins_home/web/

Pero cuidado: según tu contenedor Docker inspect, el bind-mount real apunta a:

/run/desktop/mnt/host/wsl/docker-desktop-bind-mounts/Ubuntu-22.04/... → /usr/local/apache2/htdocs

Esto puede causar problemas de sincronización entre contenedores en WSL2.
⚠️ Comprobaciones clave

    Archivos realmente copiados en el host:

Dentro del contenedor Jenkins:

docker exec -it jenkins bash
ls -l /var/jenkins_home/web

    Si ves los archivos (index.html, css/, js/, etc.), entonces Jenkins hizo bien la copia.

    Si solo ves directorios vacíos → la copia falló por permisos o rutas.

    Apache ve el volumen correcto:

Dentro del contenedor Apache:

docker exec -it apache1 bash
ls -l /usr/local/apache2/htdocs

    Debes ver exactamente los mismos archivos que Jenkins copió.

    Si ves solo Index of / → el volumen está vacío o mal montado.

🔹 Problema típico en WSL2 + Docker Desktop

    Cuando Docker Desktop monta un bind-mount desde /var/jenkins_home/web, a veces:

        Se crean permisos root vs jenkins

        Apache no puede leer los archivos (no los sirve)

        Por eso ves solo Index of /

    Solución: asegúrate que los archivos tengan permisos legibles por Apache:

docker exec -it apache1 bash
chmod -R 755 /usr/local/apache2/htdocs
chown -R www-data:www-data /usr/local/apache2/htdocs

En httpd oficial, el usuario que sirve archivos suele ser www-data o daemon.
🔹 Recomendación más robusta para tu pipeline

En lugar de copiar directamente a /var/jenkins_home/web, puedes dejar que Apache use el volumen de Jenkins como está, pero asegurándote que:

# dentro del pipeline
sh 'cp -r web/. /var/jenkins_home/web/'
sh 'chown -R 100:100 /var/jenkins_home/web'   # 100:100 suele ser www-data en contenedor httpd

    Esto garantiza que Apache tenga acceso

    Evita problemas de permisos con WSL2 bind-mounts

🔹 Alternativa “sin copy”:

Si tu web está en Git, también puedes levantar Apache directamente sobre el repo clonado, así evitas copias:

-v /var/jenkins_home/workspace/ejemplo1/web:/usr/local/apache2/htdocs/

💡 Resumen:

    “Index of /” → Apache funciona, pero no encuentra archivos que pueda leer

    Problema casi siempre: permiso o ruta del volumen

    Solución: revisar que los archivos estén dentro del contenedor Apache y sean legibles (chmod 755)

Si quieres, puedo escribirte la versión corregida de tu pipeline que:

    Copie los archivos

    Ajuste permisos

    Levante Apache

    Testee correctamente la web

Así ya no verías “Index of /” nunca más.

¿Quieres que haga eso?

Tú dijiste:
docker exec -it jenkins bash
ls -l /var/jenkins_home/webroot@e8a4b5983ea8:/# ls -l /var/jenkins_home/web
total 76
-rw-r--r-- 1 root root  8998 Feb 24 14:01 buy.html
-rw-r--r-- 1 root root  5748 Feb 24 14:01 clinic.html
-rw-r--r-- 1 root root  6492 Feb 24 14:01 contact.html
drwxr-xr-x 2 root root  4096 Feb 24 14:01 css
drwxr-xr-x 2 root root  4096 Feb 24 14:01 images
-rw-r--r-- 1 root root 20366 Feb 24 14:01 index.html
drwxr-xr-x 2 root root  4096 Feb 24 14:01 js
-rw-r--r-- 1 root root  5406 Feb 24 14:01 pet.html
-rw-r--r-- 1 root root  6991 Feb 24 14:01 service.html
root@e8a4b5983ea8:/# ls -l /usr/local/apache2/htdocs
ls: cannot access '/usr/local/apache2/htdocs': No such file or directory

ChatGPT Plus

¡Ah, perfecto! Ahora se ve claramente por qué Apache te muestra “Index of /”:

    En tu contenedor Jenkins los archivos están en /var/jenkins_home/web ✅

    En tu contenedor Apache, /usr/local/apache2/htdocs no existe ❌

Esto significa que el bind-mount entre Jenkins y Apache no se creó correctamente. En tu inspect JSON se ve que Docker Desktop/WLS está haciendo algo como:

"/run/desktop/mnt/host/wsl/docker-desktop-bind-mounts/Ubuntu-22.04/... → /usr/local/apache2/htdocs"

    Pero ese path de host es dinámico y no apunta a /var/jenkins_home/web dentro de Jenkins.

    Por eso Apache no ve los archivos y solo muestra la raíz vacía.

🔹 Soluciones posibles
1️⃣ Usar un volumen compartido “real” de Docker

Crea un volumen de Docker que compartan ambos contenedores:

docker volume create webdata

    Cambia tu pipeline para copiar los archivos ahí:

# dentro del pipeline
sh 'cp -r web/. /var/jenkins_home/web/'  # opcional, o directamente al volumen

    Levanta Apache usando el volumen:

docker run -dit \
  --name apache1 \
  -p 9001:80 \
  -v webdata:/usr/local/apache2/htdocs \
  httpd

    Esto garantiza que ambos contenedores vean los mismos archivos, sin problemas de paths de WSL2.

2️⃣ Usar el workspace de Jenkins directamente

    Cuando Jenkins clona tu repo, puedes montar directamente el path del workspace:

docker run -dit \
  --name apache1 \
  -p 9001:80 \
  -v /var/jenkins_home/workspace/ejemplo1/web:/usr/local/apache2/htdocs \
  httpd

    Así Apache ve exactamente los archivos que Jenkins tiene en su workspace.

3️⃣ Ajustar permisos

    Dentro del contenedor Apache, asegúrate de que los archivos sean legibles por el usuario que sirve HTTP (www-data):

docker exec -it apache1 bash
chown -R www-data:www-data /usr/local/apache2/htdocs
chmod -R 755 /usr/local/apache2/htdocs

💡 Tip: Evita hacer bind-mounts “complicados” de WSL2 /run/... → mejor usa:

    Docker volúmenes (recomendado)

    O paths claros dentro de /var/jenkins_home

Así nunca tendrás htdocs vacío ni problemas de sincronización.

Si quieres, puedo escribirte la versión final de tu pipeline que:

    Copie los archivos al volumen compartido

    Levante Apache con ese volumen

    Ajuste permisos automáticamente

    Testee la web

Esto haría que tu web se vea correctamente desde Jenkins y navegador.

¿Quieres que haga eso?

Tú dijiste:
puedes modificar esta pipeline: pipeline {
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

ChatGPT Plus

Perfecto. Te voy a reescribir la pipeline para que sea robusta y funcione correctamente con WSL2 y Docker:

    Usaremos un volumen Docker llamado webdata para evitar problemas de bind-mount de WSL2.

    Ajustaremos permisos para que Apache pueda leer los archivos.

    Mantendremos la entrada para AUTHOR y ENVIRONMENT.

Aquí está la versión modificada:

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
                // Crear volumen si no existe
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
                // Limpiar volumen anterior
                sh """
                docker run --rm -v ${WEB_VOLUME}:/data alpine sh -c 'rm -rf /data/*'
                """
                // Copiar archivos desde workspace al volumen
                sh """
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
                """
                // Ajustar permisos dentro del contenedor Apache
                sh """
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

✅ Qué mejora esta pipeline:

    Evita problemas con bind-mounts de WSL2: todo se hace sobre un volumen Docker (webdata).

    Permisos correctos: Apache puede leer los archivos y ya no verás “Index of /”.

    Configuración dinámica: el puerto y nombre del contenedor se manejan desde variables.

    Pipeline limpia y reutilizable: puedes cambiar el nombre del contenedor o volumen fácilmente.

Si quieres, puedo hacer una versión aún más limpia que no use contenedores intermedios Alpine para copiar archivos, y haga todo directamente dentro de Jenkins + Docker, sin pasos extra. Esto es útil para producción.

¿Quieres que haga esa versión también?


