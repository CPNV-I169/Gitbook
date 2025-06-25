# Step 01 - Déployer une image officielle

## Intention pédagogique

Dans ce laboratoire, nous allons continuer l'apprentissage des commandes Docker de base.

Nous allons entraîner:

* La récupération d'une image officielle disponible sur un "repository". ([docker image pull](https://docs.docker.com/reference/cli/docker/image/pull/))
* Utilisation de l'utilitaire de ligne de commande permettant de dialoguer avec un serveur web. ([curl](https://curl.se/))
* Construire un conteneur en utilisant une image exisante. ([docker build](https://docs.docker.com/reference/cli/docker/buildx/build/))
* Démarrer et arrêter un conteneur. ([docker container start](https://docs.docker.com/reference/cli/docker/container/start/))
* Exposer un port interne de Docker à notre machine. ([docker run --publish](https://docs.docker.com/reference/cli/docker/container/run/#publish))
* Identifier les différentes options utiles pour lancer un conteneur. ([docker run](https://docs.docker.com/reference/cli/docker/container/run/))

## Objectifs opérationnels

A la fin de ce laboratoire, vous devez obtenir ce résultat:

```bash
curl localhost:8080
```

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Welcome to nginx!</title>
        <style>
        html { color-scheme: light dark; }
        body { width: 35em; margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif; }
        </style>
    </head>
    <body>
        <h1>Welcome to nginx!</h1>
        <p>If you see this page, the nginx web server is successfully installed and
        working. Further configuration is required.</p>

        <p>For online documentation and support please refer to
        <a href="http://nginx.org/">nginx.org</a>.<br/>
        Commercial support is available at
        <a href="http://nginx.com/">nginx.com</a>.</p>

        <p><em>Thank you for using nginx.</em></p>
    </body>
</html>
```

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption><p>Résultat à obtenir via votre navigateur</p></figcaption></figure>



## Récupérer une image précise depuis un "Registry"

* Récupérer la dernière [image officielle de Nginx](https://www.docker.com/blog/how-to-use-the-official-nginx-docker-image/)

```
docker pull nginx:latest
```

{% code overflow="wrap" %}
```
latest: Pulling from library/nginx
e4fff0779e6d: Already exists
[...]
23fa5a7b99a6: Already exists
Digest: sha256:447a8665cc1dab95b1ca778e162215839ccbb9189104c79d7ec3a81e14577add
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview nginx:latest
```
{% endcode %}

* Vérifier la taille de l'image, son tag ainsi que son âge

```
docker images
```

```
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
nginx        latest    5ef79149e0ec   9 days ago   188MB
```

## Construire le conteneur

* Constuire le conteneur, sans le démarrer et en imposant un nom particulier

```docker
docker container create --name mywebserver-step-01 nginx
```

```
ca585d0d251fb0342f340523fb6b5b759a001169963 //id unique du conteneur
```

* Vérifier la bonne création, le nom ainsi que son statut

```
docker ps -a
```

{% code overflow="wrap" %}
```
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS    PORTS     NAMES
ca585d0d251f   nginx     "/docker-entrypoint.…"   11 seconds ago   Created             mywebserver-step-01
```
{% endcode %}

## Démarrer et tester le conteneur

* Démarrer le conteneur tel quel

```
docker start mywebserver-step-01
```

```
mywebserver-step-01
```

* Observer le changement d'état du conteneur, les éventuels ports d'écoute

```
docker ps -a
```

{% code overflow="wrap" %}
```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS          PORTS     NAMES
ca585d0d251f   nginx     "/docker-entrypoint.…"   5 minutes ago   Up 12 seconds   80/tcp    mywebserver-step-00
```
{% endcode %}

* Tenter d'accéder à la page d'accueil du serveur web

```
curl localhost
```

{% code overflow="wrap" %}
```
curl: (7) Failed to connect to localhost port 80 after 2250 ms: Couldn't connect to server
```
{% endcode %}

{% hint style="info" %}
La commande "container" permet d'être plus précis mais contraint également le développeur à gérer de nombreuses choses au niveau du Docker Engine, notamment la sécurité.\
\
Pour la suite de nos laboratoires, la commande "run" sera favorisée. Gardez en tête que "run" utilise, entre autre, "create" pour ce qui est de la création du conteneur.
{% endhint %}

## Nettoyer l'environnement

* Arrêter et détruiser le conteneur

```
docker stop mywebserver-step-01
```

```
mywebserver-step-01
```

```
docker rm mywebserver-step-01
```

```
mywebserver-step-01
```

{% hint style="info" %}
L'image Nginx n'a pas besoin d'être détruite pour la deuxième étape
{% endhint %}

## Créer un conteneur en ajoutant la configuration réseau

* Reconstruire et démarrer le conteneur afin de pouvoir accéder via le port 8080 à votre serveur web

```
docker run -it -d -p 8080:80 --name mywebserver-step-01 nginx
```

```
0597287b0f8dd85eb0113bcddcae356eb99a6369820b67e905957ed596339335
```

* Vérifier l'état ainsi que l'exposition du port 8080

```
docker ps -a
```

{% code overflow="wrap" %}
```
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                  NAMES
0597287b0f8d   nginx     "/docker-entrypoint.…"   58 seconds ago   Up 58 seconds   0.0.0.0:8080->80/tcp   mywebserver-step-01
```
{% endcode %}

* Tenter d'accéder à la page d'accueil ([voir le résultat attendu](step-01-deployer-une-image-officielle.md#objectifs-operationnels))
