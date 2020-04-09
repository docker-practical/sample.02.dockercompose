# Introduce

sample development with docker

Create one api app using python, one website using php.

Connect them with docker compose

following [guide](https://www.youtube.com/watch?v=Qw9zlE3t8Ko)

## Description

### Dockerfile

```bash

FROM python:3-onbuild //-> image python 3, onbuild

COPY . /usr/src/app //-> copy source from current directory

CMD [ "python", "api.py" ] //--> exec python command

```

### Docker Compose file

```bash

version: '3' //-> specific version of compose file

services:
	product-service:
		build: ./product //-> point to directory containing Dockerfile
		volumes:
			- ./product:/usr/src/app //-> map folder product
		ports:
			- 5001:80 //-> map port 5001 to 80 on container
			
    website:
        image: php:apache
        volumes:
            - ./website:/var/www/html
        ports:
            - 5000:80
        depends_on:
            - product-service //-> declare dependence
```

## Usage

### Run compose

```bash

docker-compose up

```

### Run compose with -d

To run container with demount option, container will run on background

```bash

docker-compose up -d

docker-compose stop

```