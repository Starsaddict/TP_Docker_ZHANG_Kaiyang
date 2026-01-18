## TP1 - 3
### docker version
command:
```docker --version```

result: 
```Docker version 28.3.2, build 578ccf6```

La commande docker --version permet de vérifier que Docker est bien installé sur la machine.

### docker images
command: ```docker images```

result: 
```
REPOSITORY                                                             TAG       IMAGE ID       CREATED        SIZE
pythonproject-web                                                      latest    4ecd745f282e   10 days ago    232MB
flask-hello                                                            latest    286d2c4ded67   12 days ago    223MB
nginx                                                                  latest    ca871a86d45a   2 weeks ago    244MB
mongo                                                                  7         32b5cbf6e107   4 weeks ago    1.08GB
mysql                                                                  latest    569c4128dfa6   2 months ago   1.29GB
registry.cn-shanghai.aliyuncs.com/zhinian-software/xianyu-auto-reply   1.0.2     cbfc4db109bb   4 months ago   2.99GB
hello-world                                                            latest    d4aaab6242e0   5 months ago   16.9kB
mongo                                                                  latest    a6bda40d00e5   5 months ago   1.19GB
mysql                                                                  8.0       ccf4fed7ff4b   5 months ago   1.06GB
<none>                                                                 <none>    439bfb4044dc   6 months ago   1.27GB
<none>                                                                 <none>    2426e028f770   6 months ago   1.27GB
```
Cette commande affiche les images Docker disponibles localement.
### hello-world
command: ```docker pull hello-world```

result: 
```
Using default tag: latest
latest: Pulling from library/hello-world
Digest: sha256:05813aedc15fb7b4d732e1be879d3252c1c9c25d885824f6295cab4538cb85cd
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
```

command: ```docker run hello-world```

result: 
```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
Tout est bon

### docker ps
command: `docker ps`

result: 
```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
kaiyangzhang@KaiyangdeMacBook-Air ~ % docker ps -a
CONTAINER ID   IMAGE               COMMAND                  CREATED              STATUS                          PORTS     NAMES
bec87058df8e   hello-world         "/hello"                 About a minute ago   Exited (0) About a minute ago             awesome_goldberg
4b92c7cfd3c6   pythonproject-web   "python app.py"          10 days ago          Exited (137) 6 days ago                   tp_flask
af8687a3649e   mongo:7             "docker-entrypoint.s…"   10 days ago          Exited (0) 6 days ago                     tp_mongo
d1ac409c35f1   mysql               "docker-entrypoint.s…"   2 months ago         Exited (137) 2 months ago                 mysql-test
79d27fced854   mongo               "docker-entrypoint.s…"   5 months ago         Exited (0) 5 months ago                   mongo-container
```
La commande docker ps ne montre aucun conteneur en cours d’exécution.
### docker ps -a
command: `docker ps -a`

result:
```
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS                      PORTS     NAMES
bec87058df8e   hello-world         "/hello"                 6 minutes ago   Exited (0) 6 minutes ago              awesome_goldberg
4b92c7cfd3c6   pythonproject-web   "python app.py"          10 days ago     Exited (137) 6 days ago               tp_flask
af8687a3649e   mongo:7             "docker-entrypoint.s…"   10 days ago     Exited (0) 6 days ago                 tp_mongo
d1ac409c35f1   mysql               "docker-entrypoint.s…"   2 months ago    Exited (137) 2 months ago             mysql-test
79d27fced854   mongo               "docker-entrypoint.s…"   5 months ago    Exited (0) 5 months ago               mongo-container
```
La commande docker ps -a affiche tous les conteneurs, y compris ceux qui sont arrêtés.

### docker rm <id_container>
command: `docker rm bec87058df8e`

result: `bec87058df8e`

La commande docker rm permet de supprimer un conteneur arrêté.
## TP1 - 4

command:`docker pull nginx`

result:
```bash
Using default tag: latest
latest: Pulling from library/nginx
f54f17cce8f7: Pull complete 
f43c327f6738: Pull complete 
1d5a66120144: Pull complete 
d637807aba98: Pull complete 
a178f616fffa: Pull complete 
15a5b76537aa: Pull complete 
96b249cf17a2: Pull complete 
Digest: sha256:c881927c4077710ac4b1da63b83aa163937fb47457950c267d92f7e4dedf4aec
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```
Cette commande permet de télécharger l’image officielle nginx depuis Docker Hub.

### docker run nginx
command: `docker run nginx`

result:
```bash
e72626c5a28f0397b934c93bd5ad34f5a0b62545196d26ba5e449e3dd6ee7968
```
Cette commande lance un conteneur Nginx en arrière-plan, en exposant le port 80 du conteneur sur le port 8080 de la machine locale.

### docker ps
command: `docker ps`

result:
```bash
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
e72626c5a28f   nginx     "/docker-entrypoint.…"   25 seconds ago   Up 24 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   mon_nginx
```
Le conteneur mon_nginx est en cours d’exécution et le serveur web est accessible via http://localhost:8080.

### docker stop mon_nginx
command: `docker stop mon_nginx`

result: `mon_nginx`
le conteneur mon_nginx a été arrêté avec succès

### docker rm mon_nginx
command: `docker rm mon_nginx`

result: `mon_nginx`
le conteneur mon_nginx a été supprimé avec succès

## TP1 - 5&6
### bash command:
```bash 
docker compose up --build
```

### Verification:
http://localhost:5002: 

Retourne : Flask is running

 Vérifie que l’application Flask est bien démarrée.

http://localhost:5002/healthz:

Retourne : MongoDB:OK

Vérifie que l’application Flask est correctement connectée à la base de données MongoDB.

http://localhost:5002/insert:

Retourne : Inserted:<inserted_id>

Insère un document dans la base MongoDB depuis l’application Flask.

http://localhost:5002/read:

Affiche la liste des messages stockés dans la base MongoDB.

Vérifie la lecture des données depuis la base de données.


