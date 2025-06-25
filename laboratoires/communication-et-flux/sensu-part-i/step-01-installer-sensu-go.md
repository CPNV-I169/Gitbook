# Step 01 - Installer Sensu Go

Source: [Sensu.io](https://sensu.io/?step=step-1-install-sensu-go-)

## Créer le réseau Sensu

* Lister les réseaux actuellement présents sur votre installation

```
NETWORK ID     NAME      DRIVER    SCOPE
6e7b484da597   bridge    bridge    local
bcd4a103710d   host      host      local
```

* Ajouter un réseau spécifique à Sensu

```bash
docker network create sensu
```

```
<id de votre réseau>
```

{% hint style="success" %}
Dessin : mettre à jour le schéma de votre infrastructure avec eraser.io
{% endhint %}

* Lister une nouvelle fois vos réseaux

{% hint style="info" %}
Question: Quel type de réseau avons-nous créé ?
{% endhint %}

```
NETWORK ID     NAME      DRIVER    SCOPE
6e7b484da597   bridge    bridge    local
bcd4a103710d   host      host      local
10c679c58b5d   none      null      local
545ae2592d6a   sensu     bridge    local
```

{% hint style="info" %}
Question: En vous appuyant sur la documentation officielle de Docker, valider le type de réseau par défaut que créer Docker avec la commande `docker network create`
{% endhint %}

## Créer un volume pour Sensu

* Lister les volumes existants

```
DRIVER    VOLUME NAME
//aucun volume
```

* Créer le volume qui sera dédié au backend de Sensu

```bash
docker volume create sensu-backend-data
```

```
sensu-backend-data
```

* Lister une nouvelle fois les volumes disponibles

```
DRIVER    VOLUME NAME
local     sensu-backend-data
```

## Construire et lancer le conteneur dédié au backend de Sensu

* Lister les conteneurs présents sur votre installation
* Lancer le conteneur Sensu Backend

```bash
docker run ^
-d ^
--rm ^
--name sensu-backend ^
-p 8080:8080 -p 3000:3000 ^
-v sensu-backend-data:/var/lib/sensu ^
--network sensu ^
sensu/sensu:6.11.0 sensu-backend start
```

```
Unable to find image 'sensu/sensu:6.11.0' locally
6.11.0: Pulling from sensu/sensu
a88dc8b54e91: Pull complete
[...]
b042ba88e76f: Pull complete
Digest: sha256:08030e82aa2b0c53cc04af9bc5998a94410968621a32573b9637cf718fe27357
Status: Downloaded newer image for sensu/sensu:6.11.0
82dabf3198d4b8451809cf4ea0034f5b87a482b49f3c2be8f5fe45c2ca38946d
```

* Lister une nouvelle fois les conteneurs présents sur votre installation

{% code fullWidth="true" %}
```
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS                  PORTS                                                                     NAMES
82dabf3198d4   sensu/sensu:6.11.0     "sensu-backend start"    15 seconds ago   Up 14 seconds           0.0.0.0:3000->3000/tcp, 2379-2380/tcp, 8081/tcp, 0.0.0.0:8080->8080/tcp   sensu-backend                                                                          mywebserver-step-01
```
{% endcode %}

{% hint style="success" %}
Dessin : mettre à jour le schéma de votre infrastructure avec eraser.io
{% endhint %}

## Installer l'agent

* Lancer le conteneur Sensu Agent

```bash
docker run ^
-d ^
--rm ^
--name sensu-agent ^
--network sensu ^
-p :3030 ^
sensu/sensu:6.11.0 sensu-agent start ^
--backend-url ws://sensu-backend:8081 ^
--deregister ^
--keepalive-interval=5 ^
--keepalive-warning-timeout=10 ^
--subscriptions linux
```

{% hint style="info" %}
En  vous aidant de la documentation Docker, quel est l'utilité des paramètres\
-d\
\--rm\
de la commande "docker run" ?
{% endhint %}

* Lister une nouvelle fois les conteneurs présents sur votre installation et identifier l'agent

{% code fullWidth="true" %}
```
CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS                  PORTS                                                                     NAMES
ccfb127bc70c   sensu/sensu:6.11.0     "sensu-agent start -…"   6 seconds ago        Up 6 seconds            2379-2380/tcp, 3000/tcp, 8080-8081/tcp, 0.0.0.0:54656->3030/tcp           tender_vaughan
```
{% endcode %}

## Tester l'accès à la console web Sensu

* Première requête pour voir si la console est atteignable

```bash
curl localhost:3000
```

* Puis tenter une authentification via le navigateur

| Param    | Value          |
| -------- | -------------- |
| url      | localhost:3000 |
| user     | admin          |
| password | P@ssw0rd!      |

<figure><img src="../../../.gitbook/assets/image (51).png" alt=""><figcaption><p>Ecran d'accueil de Sensu</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (52).png" alt="" width="303"><figcaption><p>Dashboard de Sensu</p></figcaption></figure>
