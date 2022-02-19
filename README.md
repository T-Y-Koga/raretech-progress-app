# ratech-progress-app

## Modify the time for wait.sh

Modify the timeout seconds in `frontend/nginx/wait.sh` if the frontend nginx server starts earlier than react. (e.g. 15 -> 120)

```
WAITFORIT_TIMEOUT=${WAITFORIT_TIMEOUT:-15}
```

##  Add file `get_random_secret_key.py` in `backend/webb-back/config`

```
from django.core.management.utils import get_random_secret_key

secret_key = get_random_secret_key()
text = 'SECRET_KEY = \'{0}\''.format(secret_key)
print(text)

```

1. `% cd backend/webb-back/config`

```
$ python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())' 
```

2. secret_key output:

```
2x$e%!k_u_0*gq0s4!_u(2(^lpy&gir0hg)q&5nurj0-sseuav
```

3. store in a .env file

```
SECRET_KEY='2x$e%!k_u_0*gq0s4!_u(2(^lpy&gir0hg)q&5nurj0-sseuav'
```

## `backend/web-back/.env` just for development

```
SECRET_KEY='XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
DEBUG=False
HOST=db
USER=user
```

## migration for database
```
$ docker-compose run --rm web-back sh -c "python3 manage.py makemigrations"

$ docker-compose run --rm web-back sh -c "python3 manage.py migrate"
```

## create superuser

```
docker-compose run --rm web-back sh -c "python3 manage.py createsuperuser"
```

## add packages

```
docker-compose run --rm web-front sh -c "yarn add next react"
```

## run server

```
docker-compose up --build 
```
