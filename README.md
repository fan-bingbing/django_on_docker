
## introduction
A complete project configuring Django to run on docker with postgres.
This projects includes development and production version of dockerfile and docker-compose file. for production environments, add on nginx serving static and media files, reverse-proxying gunicorn as production server.  

## to try this project out
My local docker version:
Docker version 19.03.6, build 369ce74a3c


This fully functioning blog app is deveopled by corey schafer using django backend for his youtube tutorial:
https://www.youtube.com/watch?v=UmljXZIypDc&list=PL-osiE80TeTtoQCKZ03TU5fNfx2UY6U4p
https://github.com/CoreyMSchafer/code_snippets/tree/master/Django_Blog/12-Password-Reset

This app supports mutiple user authentication, password reset.

before building image, update your email and password in both .env.dev and .env.prod
EMAIL_USER=***
EMAIL_PASS=***
this is used as email server sending reset email to user for user password reset. 
in case of using gmail, Access for less secure apps need to be turned on.

once email setting is done, run following commands on local machine
```bash
cd django_on_docker
docker-compose -f docker-compose.prod.yml up -d --build
docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
```

In browser visit: localhost:1337

## command cheatsheet for development 
```bash
docker-compose up -d 
docker-compose up -d --build
docker-compose logs -f
docker-compose down -v
```
## command cheatsheet for production
```bash
docker-compose -f docker-compose.prod.yml up -d --build
docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
docker-compose -f docker-compose.prod.yml logs -f
docker-compose -f docker-compose.prod.yml down -v
```

