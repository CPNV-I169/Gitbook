# Step 01 - cAdvisor

## Intentions prédagogiques

Récolter des métriques sur votre infrastructure Sensu récemment déployé dans les laboratoires précédents.

## Objectifs opérationnels

**cAdvisor** (Container Advisor) est un outil de surveillance pour Docker qui collecte des métriques sur les conteneurs en cours d'exécution (CPU, mémoire, disque, réseau).

Il s'agit de réaliser les opérations suivantes:

* [ ] Déployer le service qui collecte les métriques des conteneurs.
* [ ] Identifier les erreurs de déploiement et corriger vos scripts.
* [ ] Exploiter l'interface web pour observer les métriques.

## Tâches à réalisées

* [ ] Déployer le conteneur "cAdvisor" livré par Google

```bash
docker run ^
  --volume=/:/rootfs:ro ^
  --volume=/var/run:/var/run:ro ^
  --volume=/sys:/sys:ro ^
  --volume=/var/lib/docker/:/var/lib/docker:ro ^
  --volume=/dev/disk/:/dev/disk:ro ^
  --publish=8080:8080 ^
  --detach=true ^
  --name=cadvisor ^
  google/cadvisor:latest
```

```
<id de votre conteneur>
```

* [ ] Identifier les erreurs de déploiement et corriger vos scripts

- !!! Le port 8080 de votre machine local est déjà attribué (voir la config sensu).

{% code overflow="wrap" %}
```
docker: Error response from daemon: driver failed programming external connectivity on endpoint cadvisor (bc3338ebb6db6ad5840ed897eb29c876b104a9d6ccf500358f1d52fd09898db0): Bind for 0.0.0.0:8080 failed: port is already allocated.
```
{% endcode %}

* !!! Tentative de déploiement en utilisant un nom de conteneur déjà réservé

{% code overflow="wrap" %}
```
docker: Error response from daemon: Conflict. The container name "/cadvisor" is already in use by container "c5c307c2a7218bcc40768446b70ea64ca3c1208b80c8281816fe7462d7051971". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
```
{% endcode %}

* [ ] Accéder à l'interface web pour observer les métriques

- Atteindre la page d'accueil

```
http://localhost:<votrePort>
```

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption><p>Page d'accueil de cAdvisor</p></figcaption></figure>

* Atteindre la page spécifique pour le conteneur Sensu Backend

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption><p>Page spécifique pour le conteneur Sensu Backend</p></figcaption></figure>
