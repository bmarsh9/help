## Flask

##### Run
```
python3 manage.py runserver -h 0.0.0.0 -p 5000
flask run --cert adhoc -h 0.0.0.0
gunicorn --bind 0.0.0.0:5000 flask_app:app --access-logfile '-' --error-logfile "-"
```

##### Common migrations
```
python3 manage.py db migrate
python3 manage.py db upgrade
python3 manage.py db stamp head
```

## Gunicorn
```
gunicorn --bind 0.0.0.0:5000 flask_app:app --access-logfile '-' --error-logfile "-"
```

## Docker

##### Docker daemon in WSL
```
sudo dockerd &
```

##### Common commands
```
docker build --tag app:1.0.0 .
docker exec -it app bash
docker run -it -d -p 5000:5000 app
```

##### Sample Dockerfile for python
```
FROM python:3.8-slim-buster

WORKDIR /app

# for postgres connection
RUN apt-get update \
    && apt-get -y install libpq-dev gcc \
    && pip3 install psycopg2

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

CMD ["/bin/bash","run.sh"]
```

##### Sample docker-compose.yml for flask
```
version: '3'
services:
  app:
    container_name: app
    image: app
    depends_on:
      - postgres
    networks:
      - db_nw
      - web_nw
    ports:
      - "5000:5000"
    restart: unless-stopped
    environment:
      - SQLALCHEMY_DATABASE_URI=postgresql://${POSTGRES_USER:-db1}:${POSTGRES_PASSWORD:-db1}@${POSTGRES_HOST:-postgres}/${POSTGRES_DB:-db1}
      - DEFAULT_EMAIL=${DEFAULT_EMAIL:-admin@example.com}
      - DEFAULT_PASSWORD=${DEFAULT_PASSWORD:-admin}
      - SETUP_DB=${SETUP_DB:-no}
      - POSTGRES_DB=${POSTGRES_DB:-db1}
      - VERSION=${VERSION:-1.0.0}
  postgres:
    container_name: postgres
    image: postgres
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-db1}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-db1}
      POSTGRES_DB: ${POSTGRES_DB:-db1}
      PGDATA: /data/postgres
    #volumes:
    #   - postgres:/data/postgres
    #ports:
    #  - "5432:5432"
    networks:
      - db_nw
    restart: unless-stopped

networks:
  db_nw:
    driver: bridge
  web_nw:
    driver: bridge
volumes:
  dbdata:
```

## Git

##### Common
```
git pull
git checkout -b new-branch
git add . 
git commit -m "my changes"
git push origin new-branch
```

##### Undo commit
```
git commit -m "Something terribly misguided" # (0: Your Accident)
git reset HEAD~                              # (1)
[ edit files as necessary ]                    # (2)
git add .                                    # (3)
git commit -c ORIG_HEAD                      # (4)
```

## K8

## Terraform

##### Tfswitch
```
https://tfswitch.warrensbox.com/Install/
```

## VirtualEnv
```
python3 -m venv venv
source venv/bin/activate
```

## Gcloud

##### Cheat sheet
```
https://gist.github.com/bmarsh9/3a54ba90100d20529c9567b450af66ec
```
##### Common commands
```
gcloud auth application-default login

gcloud config list
gcloud auth list
gcloud config set project $MY_PROJECT_ID

gcloud projects list
gcloud organizations list

#switch project based on the name
gcloud config set project $(gcloud projects list --filter='name:wordpress-dev' --format='value(project_id)')
```

##### Tunneling
```
gcloud compute start-iap-tunnel test-vdi 3389 --local-host-port=localhost:5000 --zone us-west1-b
```

##### SSH
```
gcloud compute ssh --zone "us-west1-b" "sonarqube" --project "security-project-console"
```

##### Tunneling via SSH
```
gcloud compute ssh --zone "us-west1-b" "sonarqube" --project "security-project-console" -- -NL 8081:localhost:9000
```

## Cloud Naming
```
https://stepan.wtf/cloud-naming-convention/
```



