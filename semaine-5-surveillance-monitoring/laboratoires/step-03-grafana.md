# Step 03 - Grafana

## Intentions prédagogiques

Améliorer le visuel d'un outil existant en ajoutant un composant et en le connectant sur la source de données.

## Objectifs opérationnels

Pour une visualisation plus agréable, **Grafana** s'intègre très bien avec Prometheus.

En nous appuyant sur cAdvisor installé dans l'étape précédente, ainsi que Prometheus, nous allons pouvoir améliorer le visuel.

Il s'agit de réaliser les opérations suivantes:

* [ ] Déployer le conteneur Grafana.
* [ ] Ajouter une source de données (via l'interface d'administration web).
* [ ] Importer des éléments graphiques (widgets) pré-configuré pour Docker afin de construire un Dashboard convivial.
* [ ] Exploiter l'interface web pour observer les métriques et obtenir un tableau de bord convivial.

## Tâches à réalisées

* [Source officielles](https://prometheus.io/docs/visualization/grafana/)

- [ ] Déployer le conteneur Grafana

```bash
docker run -d -p 3000:3000 --name=grafana grafana/grafana
```

* [ ] Ajouter une source de données (via l'interface d'administration web).

- Accéder à la console administrateur

{% hint style="info" %}
Accès à la console :\
user : admin

pwd : admin (à changer dès la première authentification)
{% endhint %}

* Ajouter une source de données

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>



{% hint style="info" %}
L'url de Prometheus à renseigner est le suivant:\
\
[http://host.docker.internal:9090](http://host.docker.internal:9090)
{% endhint %}

* [ ] Importer des éléments graphiques (widgets) pré-configuré pour Docker afin de construire un Dashboard convivial.

- Ajouter un dashboard préconfiguré pour Prometheus

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption><p>Ajout d'un dashboard pour Prometheus</p></figcaption></figure>

* [ ] Exploiter l'interface web pour observer les métriques et obtenir un tableau de bord convivial.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>
