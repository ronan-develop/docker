# Docker

[//]: # ()

[//]: # (- run deamon :`dockerd`)

[//]: # (- reload daemon : `sudo systemctl daemon-reload`)

[//]: # (- list images :`docker images`)

[//]: # (- list available &#40;launched&#41; containers:`docker ps`)

[//]: # (- download existing image from local or dockerhub : `docker pull nomImage`)

[//]: # (- launch image :`docker run -it nomImage`)

[//]: # (- stop container :`docker ps` copy id and `docker stop {id}`)

[//]: # (- stop all containers :`docker stop $&#40;docker ps -a -q&#41;`)

[//]: # (- run container as daemon :`docker run -it -d nomImage`)

[//]: # (- clean :`docker system prune`)

[//]: # (- remove image :`sudo docker image rm -f nomImage`)

[//]: # (- list networks :`docker network ls`)

[//]: # ()

[//]: # (## Launch)

[//]: # (image prestashop + image mysql que je vais lier dans un container)

[//]: # (lancer les deux id créés)

[//]: # ()

[//]: # (docker ps -a to list container)

[//]: # (- docker start `3 fisrt chars of containers id`)

[Docker compose course](./docker-compose/docker-compose.md)
## Manipuler les containers

Un container est un simple (ou un ensemble) de processus au niveau du system.
Ces process ont pour vocation de faire tourner le code qui est prévu dans l'image.

### Eviter le sudo

```bash
sudo usermod -aG docker $USER
```

### Lancer un container en mode detached

```bash
# docker run -d --name typeContainerName image:flag
# example :
docker run -d --name c1 nginx:latest
flag -ti # lance un terminale sur le process
flag -p # exposition de port
flag --rm # suppression du container sur sortie
flag --hostname # change le nom du host dans la console du container
flag --dns spécifier des dns qui ne seraient pas utilisés dans le container

```
### Lister tous les containers
```bash
docker ps -a
```

### Lister les container actifs
```bash
docker ps
```

### Lister les id des containers actif
```bash
docker ps -q
```

### Lister les id des containers
```bash
docker ps -qa
```

### Imbriquer des commandes
```bash
# forcer suppr des containers actif
docker rm -f $(docker ps -q)
# suppr la totalité des container sur la machine
docker rm -f $(docker ps -qa)
```

### Démarrer un container
```bash
docker start # nom
```
### Stopper un container
```bash
docker stop # nom
```

