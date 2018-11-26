# Vespene docker

Basic example howto run [vespene ci](https://github.com/vespene-io/vespene) in docker.

### Clone
```
git clone git@github.com:pyToshka/vespene-docker.git
cd vespene-docker
```

### Building and running

For building and running you can use docker-compose, before using need to set up environments in docker compose file and build new application.

Example of environments

| Var name  | Descriptio   |
|---|---|
|  DB_NAME |  Name of vespene database |
| DB_USER  | Username for pg database   |
| DB_PASS  | Database password  |
|  DB_HOST | Database hostname for connection  |
| BUILDROOT  |  build root path |
| BUILDROOT_WEB_LINK | Web link for build root|


When you have set up docker compose, you be able to build and run application

### How To build
All commands should run from repository folder
Run
```
docker-compose up -d --build
```
For getting status

Run
```
docker-compose logs -f
```
### How To make migration
Run
```
docker-compose run vespene python manage.py migrate
```


### How To create new superuser
Run
```
docker-compose run vespene python manage.py createsuperuser
```

### How To deploy tutorial
Run
```
docker-compose run vespene python manage.py tutorial_setup
```

### Other commands

Get list of command:

Run
```
docker-compose run vespene python manage.py
```

Executing command
```
docker-compose run vespene python manage.py command
```


### Ports
By default application will be available on `8080` port


Enjoy
