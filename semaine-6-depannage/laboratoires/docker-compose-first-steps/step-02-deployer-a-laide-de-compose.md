# STEP 02 - Déployer à l'aide de compose

* Créer un fichier "compose.yaml" et y intégrer le contenu suivant:

```docker
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"
```

* Exploiter le fichier composer pour constuire son infrastructure

```
docker compose up
```

* Une fois le déploiement réalisé, testez-la via curl

```
curl localhost:8000
```

```
Hello World! I have been seen 1 times.
```

* Répéter l'expérience afin de voir le nombre de fois s'incrémenter
* En utilisant les commandes habituelles, identifier les composants qui ont été déployés par Compose.

- [ ] les images
- [ ] les volumes
- [ ] les réseaux
- [ ] les conteneurs

* Dessiner l'infra à l'aide de Eraser
