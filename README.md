# Ghostwriter

[![Python Version](https://img.shields.io/badge/Python-3.7-brightgreen.svg)](.) [![License](https://img.shields.io/badge/License-BSD3-darkred.svg)](.) [![Black Hat Arsenal 2019](https://img.shields.io/badge/2019-Black%20Hat%20Arsenal-lightgrey.svg)](.)

![ghostwriter](https://github.com/GhostManager/Ghostwriter/raw/master/DOCS/images/logo.png)

Ghostwriter is a Django project written in Python 3.7 and is designed to be used by a team of operators. The platform is made up of several Django apps that own different roles but work together. See the Wiki for more information.

## Install

### Local
```
mkdir .envs && cp -r .envs_template/.* .envs
docker-compose -f local.yml stop; docker-compose -f local.yml rm -f; docker-compose -f local.yml build; docker-compose -f local.yml up -d
docker-compose -f local.yml run --rm django /seed_data
docker-compose -f local.yml run --rm django python manage.py createsuperuser
```

### Prod
```
mkdir .envs && cp -r .envs_template/.* .envs
cd ssl
openssl req -new -newkey rsa:4096 -days 365 -nodes -x509 -subj "/O=Ghostwriter/CN=ghostwriter.local" -keyout ghostwriter.key -out ghostwriter.crt
openssl dhparam -out dhparam.pem 4096
cd ..
docker-compose -f production.yml stop; docker-compose -f production.yml rm -f; docker-compose -f production.yml build; docker-compose -f production.yml up -d
docker-compose -f production.yml run --rm django /seed_data
docker-compose -f production.yml run --rm django python manage.py createsuperuser
```
