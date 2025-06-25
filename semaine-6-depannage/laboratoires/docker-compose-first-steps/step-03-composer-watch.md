# STEP 03 - Composer watch

* Modifier le fichier "compose.yaml" en ajoutant une librairie pour le développement avec compose, "Compose Watch".

```docker
services:
  web:
    build: .
    ports:
      - "8000:5000"
    develop:
      watch:
        - action: sync
          path: .
          target: /code
  redis:
    image: "redis:alpine"
```

* Stopper le déploiement (ctrl c dans la console dédiée)
* Relancer le dépoiement ainsi:

```docker
docker compose up --watch
```

* Revalider le bon fonctionnement de l'application

```
curl localhost:8000
```

```
Hello World! I have been seen 6 times.
```

* Réaliser une modification dans le code pour voir si "watch" se comporte comme attendu en redéployant l'application sans que nous ayons besoin d'intervenir

```
vi app.py
```

* Modifier le "Hello World!" en "Hello MyFirstname" (pour l'exemple j'ai utiliser "Hello Docker"
* Retester l'application

```
Hello Docker! I have been seen 7 times.
```

