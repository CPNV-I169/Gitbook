# Step 02 - Prometheus

## Intentions prédagogiques

Configurer un outil open source permettant la collecte d'information, mais aussi l'envoi d'alerte lorsque des comportements inattendus sont détectés.

## Objectifs opérationnels

Prometheus est un outil de surveillance pour tous types d'infrastructure, très bien adapté pour Docker.

En nous appuyant sur cAdvisor installé dans l'étape précédente, nous allons pouvoir mettre à disposition les métriques à Prometheus.

Il s'agit de réaliser les opérations suivantes:

* [ ] Créer un fichier de paramétrage de base pour Prometheus.
* [ ] Déployer le conteneur Prometheus en injectant le fichier de paramétrage.
* [ ] Exploiter l'interface web pour observer les métriques.

## Tâches à réalisées

* [Sources officielles](https://prometheus.io/docs/prometheus/latest/installation/)

- [ ] Créer un fichier de paramétrage de base pour Prometheus

* Réaliser les commandes suivantes pour créer un répertoire, se postionner à l'intérieur et créer un fichier "yaml" et l'ouvrir pour le modifier.

```
mkdir prometheus
cd prometheus
vi prometheus.yml
```

* Ajouter le contenu suivant:

{% hint style="info" %}
Avant de saisir le contenu, passer vi en mode "insertion" en appuyant sur "i".\
En bas à gauche de votre écran vous verrez le mode " -- INSERT --" apparaître.
{% endhint %}

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'cadvisor'
    static_configs:
      - targets: ['cadvisor:8080']
```

{% hint style="warning" %}
* **scrape\_interval** défini la cadence de récupération de métriques par Prometheus.
* **targets** mentionne la cible qui expose les métriques à récupérer.
{% endhint %}

{% hint style="info" %}
Pour quitter l'éditeur "vi".\
\
"ESC" pour quitter le mode édition

maj + ":" et saisir "wq" pour "write and quit"
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Pour quitter vi en prenant en compte les modifications</p></figcaption></figure>

* [ ] Déployer le conteneur Prometheus en"bind-mount" le fichier de paramétrage.

```bash
docker run ^
    -d ^
    --name=prometheus ^
    -p 9090:9090 ^
    -v ./prometheus.yml:/etc/prometheus/prometheus ^
    prom/prometheus
```

* [ ] Configurer la persistence de données et appliquer le paramètrage
  * [ ] Le fichier prometheus va être "bind-mounted" dans /etc/prometheus
  * [ ] Le volume pour les données est créé puis ensuite attaché lors du processus de démarrage du conteneur.

```bash
docker volume create prometheus-data
```

```bash
docker run ^
    -d ^
    -p 9090:9090 ^
    --name=prometheus ^
    -v ./prometheus.yml:/etc/prometheus/prometheus ^
    -v prometheus-data:/prometheus ^
    prom/prometheus
```

* [ ] Exploiter l'interface web pour observer les métriques

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption><p>Dashboard de Prometheus, localhost:9090</p></figcaption></figure>

