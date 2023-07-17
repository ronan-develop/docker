[[# Docker compose

La structure de ce fichier `yaml` comporte :

- La version de docker que l'on souhaite utiliser
- Les services qui sont les application à faire tourner dans le container.

```yaml

# La version de docker que l'on souhaite
version: '3'
# Les services
services:
  ###> doctrine/doctrine-bundle ###
  database:
    image: 'mariadb:latest'
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: snowtricks
    ports:
      # To allow the host machine to access the ports below, modify the lines below.
      # For example, to allow the host to connect to port 3306 on the container, you would change
      # "3306" to "3306:3306". Where the first port is exposed to the host and the second is the container port.
      # See https://docs.docker.com/compose/compose-file/compose-file-v3/#ports for more information.
      - '3306'
      # You may use a bind-mounted host directory instead, so that it is harder to accidentally remove the volume and lose all your data!
      # - ./docker/db/data:/var/lib/postgresql/data:rw
  ###< doctrine/doctrine-bundle ###

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: pma
    links:
      - database
    # password is the same as database (password)
    environment:
      PMA_HOST: database
      PMA_PORT: 3306
      PMA_ARBITRARY: 1
    restart: always
    ports:
      - "8081:80"

volumes:
  ###> doctrine/doctrine-bundle ###
  db-data:
  ###< doctrine/doctrine-bundle ###
```

## Commandes :

|           Actions           |                  Commandes                  |
|:---------------------------:|:-------------------------------------------:|
| builder et lancer en daemon |         ```docker-compose up -d ```         |
|     lancer les services     | ```docker start``` + nom ou id du container |
|    stopper les services     |              ```docker stop```              |
|     lister les services     |    ```docker ps -a``` ou ```docker ps```    |

## Etapes

Etapes à suivres pour construire un `docker-compose.yaml`

```yaml
version : '3.9'
services :
  apache :
    image : httpd:latest
    container_name : my-apache-app
    ports :
      - '8080:80'
    volumes :
      - ./website:/usr/local/apache2/htdocs
```

### Bénéfices

Une commande Docker `run` peut rapidement devenir longue quand on fait références a des
volumes des variables d'environnement, des mots de passe, etc.
Ces commandes peuvent être utilisées plusieurs fois par jour, ce qui peut être fastidieux.

