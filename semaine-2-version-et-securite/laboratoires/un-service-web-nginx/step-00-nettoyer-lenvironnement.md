# Step 00 - Nettoyer l'environnement

## Intention pédagogique

Dans ce laboratoire, nous allons entraîner les diverses commandes pour "nettoyer" votre environnement Docker.

Les familles de commandes suivantes vont être entraînées:

* Lister les conteneurs et les images présentes ([docker ps](https://docs.docker.com/reference/cli/docker/container/ls/)).
* Arrêter des conteneurs en cours d'exécution ([docker images](https://docs.docker.com/reference/cli/docker/image/ls/)).
* Détruire:
  * des conteneurs ([docker rm](https://docs.docker.com/reference/cli/docker/container/rm/)).
  * &#x20;des images ([docker rmi](https://docs.docker.com/reference/cli/docker/image/rm/)).

## Objectifs opérationnels

Le résultat a obtenir à la fin du laboratoire

* [ ] Plus aucun conteneur présent (sauf des conteneurs dont vous auriez besoin pour d'autres modules bien entendu)

```
docker ps -a
```

```docker
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

* [ ] Plus aucune image (sauf des images dont vous auriez besoin pour d'autres modules bien entendu)

```
docker images
```

```
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE

```

## TODO

### Prérequis

* Lancer Docker Desktop pour démarrer le Docker Engine

### Vérifier l'état d'un conteneur

* Vérifier que plus aucun contener "nginx" ne soit exécuté

```docker
docker ps -a
```

### Stopper un conteneur

* Si des conteneurs sont encore actifs, arrêtez-les !

```docker
docker stop <nom du conteneur à stopper>
```

### Supprimer un conteneur

* Si des conteneurs sont encore présents, détruisez-les !

```
docker rm <nom du conteneur à détruire>
```

### Supprimer une image

* Si des images sont présentes, les détruire

```
docker rmi <nom de l'image à détruire>
```

