# Step 02 - Publier du contenu web sur son conteneur Nginx

## Intention pédagogique

Dans ce laboratoire, nous allons récupérer un contenu web simple et le publier sur notre serveur web nginx "contenerisé".

Nous allons entraîner:

* Récupérer et adapter un "template" de login.
* L'ajout d'une couche logique (layer) à une image existante. ([docker layer](https://docs.docker.com/build/guide/layers/)) ([docker dockerfile](https://docs.docker.com/reference/dockerfile/))
* Re-construire un conteneur et le démarrer ([docker run](https://docs.docker.com/reference/cli/docker/container/run/)).
* Servir le contenu html  via le conteneur.

## Objectifs opérationnels

A la fin du laboratoire, cette page supplémentaire doit pouvoir être appellé ainsi:

```
localhost:8080/login.html
```

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Résultat à obtenir pour la page /login<br></p></figcaption></figure>

{% hint style="danger" %}
La page d'accueil doit toujours être disponible via localhost:8080 !
{% endhint %}

## Prérequis

* [ ] Avoir terminé l'étape précédente, "[Step 01 - Déployer une image officielle](step-01-deployer-une-image-officielle.md)"
* [ ] Disposer en local du template HTML/CSS que nous utiliserons comme page d'accès pour nos membres.

{% file src="../../../.gitbook/assets/login-form-v1.zip" %}
Source : [Colorlib](https://colorlib.com/wp/template/login-form-v1/)
{% endfile %}

## Comment publier du contenu sur NGINX

Mettons temporairement de côté Docker. Si vous disposions d'une installation NGINX "classique", nous devrions identifier le répertoire dans lequel nous devrions déposer le contenu à publier pour nos utilisateurs web.

Ce chemin est le suivant:

```
/usr/share/nginx/html
```

C'est également ce chemin qui sera utilisé, au sein de notre conteneur, pour publier notre page login.

{% hint style="info" %}
Comment copier du contenu présent sur notre machine local (Docker host) dans notre conteneur ? Nous étudierons cela à l'étape suivante.
{% endhint %}

## Préparer le répertoire de travail

Note : utiliser cmder pour réaliser ce travail

* [ ] Créer un répertoire "CustomNginx"
  * [ ] Créer un fichier "Dockerfile" vide
  * [ ] Créer un répertoire html
  * [ ] Décompresser template html livré
    * [ ] Ne garder que le contenu présent dans le sous-répertoire "Login-v1"
    * [ ] Renommer "Login-v1" en "login

#### Voici le résultat à obtenir:

```
│   Dockerfile          //ce fichier permettra de personnaliser nginx
├───html                //ce répertoire contiendra tout le contenu html à ajouter
│   └───login           //contenu login du template
│       │   login.html      //à renommer (index.html)
│       ├───css
│       ├───fonts
│       ├───images
│       ├───js
│       └───vendor
```

## Un premier Dockefile

Note : utiliser Visual Studio Code pour réaliser ce travail

Actuellement nous avons récupéré (docker pull) une image existante sur le registry publique DockerHub.

Dans ce laboratoire nous aimerions, en partant de cette même image, ajouter une ou plusieurs couches (layer) afin de publier du contenu web personnalisé (la page login).

* [ ] Ouvrir le répertoire "CustomNginx" dans Visual Studio Code et éventuellement valider cet emplacement (trust folder)

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption><p>Validation de sécurité du répertoire "CustomNginx"</p></figcaption></figure>

* [ ] Intégrer ce contenu dans le fichier DockerFile

```docker
# syntax=docker/dockerfile:1

FROM nginx:latest

COPY ./html/login /usr/share/nginx/html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
```

#### Explications

```docker
# syntax=docker/dockerfile:1               //version du langage utilisé

FROM nginx:latest                          //image de base pour notre propre image

COPY ./html/login /usr/share/nginx/html    //mis à disposition des fichiers "login"

EXPOSE 8080                                //information mentionnant l'utilisation du port 8080

CMD ["nginx", "-g", "daemon off;"]         //demande à Nginx de s'exécuter au premier plan
```

* Source : [Nginx in the foreground](https://www.uptimia.com/questions/how-to-run-nginx-in-the-foreground-within-a-docker-container)

## Déployement

* [ ] Construire notre image personnalisée en exploitant notre DockerFile

```
docker build -t nginx-custom-step-01 .
```

```
[+] Building 0.7s (9/9) FINISHED                                                                                                                                                 docker:desktop-linux 
[...]
 => [internal] load metadata for docker.io/library/nginx:latest                                                                                                                                  0.0s 
 => [internal] load .dockerignore                                                                                                                                                                0.0s 
 => => transferring context: 2B                                                                                                                                                                  0.0s 
 => [internal] load build context                                                                                                                                                                0.0s 
 => => transferring context: 8.49kB                                                                                                                                                              0.0s 
 => CACHED [1/2] FROM docker.io/library/nginx:latest                                                                                                                                             0.0s 
 => [2/2] COPY ./html/login /usr/share/nginx/html                                                                                                                                                0.0s 
 => exporting to image                                                                                                                                                                           0.1s
 => => exporting layers                                                                                                                                                                          0.1s 
 => => writing image sha256:d087501965fa441f7e4d2c5b085ab1126ea45f96151decd7c8184199d5067a59                                                                                                     0.0s 
 => => naming to docker.io/library/nginx-custom-step-01                                                                                                                                          0.0s 

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview 

```

* [ ] Valider que l'image est bien disponible

```
docker images
```

```
REPOSITORY             TAG       IMAGE ID       CREATED         SIZE
nginx-custom-step-01   latest    d087501965fa   8 seconds ago   199MB  //différence de taille
nginx                  latest    5ef79149e0ec   10 days ago     188MB
```

* [ ] Constuire et démarrer le conteneur

```
docker run -d --name mywebserver-step-01 -p 8080:80 nginx-custom-step-01
```

```
<identifiant unique de votre docker>
```

* [ ] Vérifier l'exposition du port 80 via le 8080

```
docker ps -a
```

{% code fullWidth="true" %}
```
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS                      PORTS     NAMES
1196e62fa220   nginx-custom-step-01   "/docker-entrypoint.…"   10 seconds ago   Up 9 seconds   8080/tcp, 0.0.0.0:8080->80/tcp   mywebserver-step-01
```
{% endcode %}

## Test le résultat

* [ ] la page de base de Nginx est toujours disponible

```
curl localhost:8080
```

```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
[...]
<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

* [ ] la page de login est maintenant disponible

```
curl localhost:8080/login.html
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
        <title>Login V1</title>
        [...]
        </head>
<body>
        <div class="limiter">
                <div class="container-login100">
                        <div class="wrap-login100">
                                <div class="login100-pic js-tilt" data-tilt>
                                        <img src="images/img-01.png" alt="IMG">
                                </div>

                                <form class="login100-form validate-form">
                                        <span class="login100-form-title">
                                                Member Login
                                        </span>
[...]

                                        <div class="container-login100-form-btn">
                                                <button class="login100-form-btn">
                                                        Login
                                                </button>
                                        </div>

                                        <div class="text-center p-t-12">
                                                <span class="txt1">
                                                        Forgot
                                                </span>
                                                <a class="txt2" href="#">
                                                        Username / Password?
                                                </a>
                                        </div>
[...]
</body>
</html>
```

[Voir le visuel à obtenir depuis le navigateur.](step-02-publier-du-contenu-web-sur-son-conteneur-nginx.md#objectifs-operationnels)
