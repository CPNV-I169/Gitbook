# Première tentative

## Consignes

### Objectif:

Il s'agira dans ce laboratoire de déployer un serveur web (NGINX) sur votre Docker Engine local.

Les manipulations suivantes seront entraînées:

* Lister les conteneurs et voir leur statut.
* Récupérer une image existante sur Docker Hub et contruire un premier conteneur.
* Déployer le conteneur et tenter d'accéder à la page par défaut de serveur web.

### Aide: <a href="#aide" id="aide"></a>

Toutes les étapes sont documentées ci-dessous. Ce ne sera pas le cas pour les laboratoires suivants donc prenez bien le temps de comprendre ce que vous réalisez.

### Mode collaboratif <a href="#mode-collaboratif" id="mode-collaboratif"></a>

Vous pouvez réaliser ce travail à deux. Mais chacun met en place son propre environnement.

### Temps à disposition <a href="#temps-a-disposition" id="temps-a-disposition"></a>

30 minutes.

### Livrable <a href="#livrable" id="livrable"></a>

Réaliser une documentation d'installation. Favoriser une documentation basée sur des lignes de commandes en mentionnant les "inputs" et les "outputs" attendus. Ne faites des captures d'écran que lorsque la ligne de commandes n'est pas possible.En cas de pannes, documenter la résolution.La documentation à produire est pour vous, afin d'être capable de remettre en place votre système en cas de panne par exemple.

## Réalisation

### Prérequis

* [ ] WSL2 est installé et opérationnel
* [ ] Docker Desktop est lancé
* [ ] Accès au web

### Récupérer l'image officielle NGINX pour Docker

[Source](https://hub.docker.com/_/nginx)

* Lister les images présentes sur votre environnement local (le résultat est vide)

```docker
docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

* Pull l'image (observer les actions réalisées par Docker)

```
docker pull nginx

Using default tag: latest
latest: Pulling from library/nginx
e4fff0779e6d: Pull complete
2a0cb278fd9f: Pull complete
7045d6c32ae2: Pull complete
03de31afb035: Pull complete
0f17be8dcff2: Pull complete
14b7e5e8f394: Pull complete
23fa5a7b99a6: Pull complete
Digest: sha256:447a8665cc1dab95b1ca778e162215839ccbb9189104c79d7ec3a81e14577add
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview nginx
```

{% hint style="info" %}
Quelle est la version de l'image NGINX qui a été récupérée ?
{% endhint %}

* Lister une nouvelle fois les images

```
docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
nginx        latest    5ef79149e0ec   2 days ago   188MB
```

{% hint style="info" %}
Quel est le poids de cette image ?\
Que contient-elle à votre avis ?\
La valuer de l'attribut "CREATED" ne vous intrigue-t-il pas ?
{% endhint %}

### Déployement - première tentative

* Déployer notre conteneur Nginx.

```
docker run --name nginx-first-attempt nginx

/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/08/17 15:33:22 [notice] 1#1: using the "epoll" event method
2024/08/17 15:33:22 [notice] 1#1: nginx/1.27.1
2024/08/17 15:33:22 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/08/17 15:33:22 [notice] 1#1: OS: Linux 5.15.153.1-microsoft-standard-WSL2
2024/08/17 15:33:22 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/08/17 15:33:22 [notice] 1#1: start worker processes
2024/08/17 15:33:22 [notice] 1#1: start worker process 29
2024/08/17 15:33:22 [notice] 1#1: start worker process 30
2024/08/17 15:33:22 [notice] 1#1: start worker process 31
2024/08/17 15:33:22 [notice] 1#1: start worker process 32
2024/08/17 15:33:22 [notice] 1#1: start worker process 33
2024/08/17 15:33:22 [notice] 1#1: start worker process 34
2024/08/17 15:33:22 [notice] 1#1: start worker process 35
2024/08/17 15:33:22 [notice] 1#1: start worker process 36
2024/08/17 15:33:22 [notice] 1#1: start worker process 37
2024/08/17 15:33:22 [notice] 1#1: start worker process 38
2024/08/17 15:33:22 [notice] 1#1: start worker process 39
2024/08/17 15:33:22 [notice] 1#1: start worker process 40
```

{% hint style="info" %}
La commande ne semble être bloquée... si vous lancez un second terminal cmder, lister les conteneurs. Qu'observez-vous ?
{% endhint %}

```
docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
e978621d81ce   nginx     "/docker-entrypoint.…"   6 seconds ago   Up 5 seconds   80/tcp    nginx-first-attempt
```

* Tenter de contacter le serveur web (apparemment il écoute sur le port 80, en tcp)

```
curl localhost
curl: (7) Failed to connect to localhost port 80 after 2256 ms: Couldn't connect to server
```



{% hint style="warning" %}
Conclusions après cette première tentative\
\
\* le conteneur a été construit + exécuté... il serait intéressant de pouvoir faire les deux séparemment.\
\* je suis constraint de laisser un prompte cmder ouvert pour que le conteneur s'éxecute... ce n'est pas possible en production.\
\* impossible d'atteindre le serveur web sur le port 80... alors qu'il semble bien écouter ce port.
{% endhint %}

### Stopper et supprimer le conteneur

* Lister les conteneurs et récupérer le nom (ou l'id du conteneur)

```
docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
e978621d81ce   nginx     "/docker-entrypoint.…"   6 seconds ago   Up 5 seconds   80/tcp    nginx-first-attempt
```

* Stopper le conteneur et vérifier son état

```
docker stop nginx-first-attempt
nginx-first-attempt
```

```
docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                     PORTS     NAMES
e978621d81ce   nginx     "/docker-entrypoint.…"   10 minutes ago   Exited (0) 3 seconds ago             nginx-first-attempt
```

{% hint style="info" %}
Le conteneur mentionne "Exited" et le port a été libéré !
{% endhint %}

* Supprimer le conteneur

```
docker rm nginx-first-attempt
nginx-first-attempt
```

```
docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

* Valider que l'image est toujours présente

```
docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
nginx        latest    5ef79149e0ec   2 days ago   188MB
```
