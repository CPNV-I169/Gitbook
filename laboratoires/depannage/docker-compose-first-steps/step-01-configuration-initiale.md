# STEP 01 - Configuration initiale

* Créer un répertoire dédié pour le laboratoire

```
mkdir composeFirstAttempt
cd composeFirstAttempt
```

* Créer un fichier "app.py" et y insérer le code présenté ci-dessous:

```
touch app.py
```

```python
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

* Créer un deuxième fichier "requirements.txt" et intégrer le contenu suivant:

```
touch requirements.txt
```

```
flask
redis
```

* Créer un troisième fichier "Dockerfile" et intégrer le contenu suivant:

```docker
# syntax=docker/dockerfile:1
FROM python:3.10-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run", "--debug"]
```
