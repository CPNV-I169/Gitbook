# Détection d'erreurs

## Introduction

Le dépannage sur une infrastructure conteneurisée implique une approche méthodique. Il est important, avant de prendre des dispositions, d'avoir bien étudié les différents niveaux qui peuvent être la ou les sources des erreurs détectées.

Voici une approche, étape par étape, pour détecter rapidement les pannes et erreurs sur vos environnements.

## Etape 1 - Première analyse

## Obtenir une vue d'ensemble de votre infrastructure

* **Identifier les symptômes** : Commence par collecter un maximum d’informations. Quels sont les symptômes du problème ? Le conteneur ne démarre pas, il plante après un certain temps, ou il y a des problèmes de connectivité ?
* **Contexte** : S'agit-il d'un problème spécifique à un conteneur, une image, ou un composant externe (réseau, volumes, etc.) ?

## Récolter les informations "facilement" accessibles

* **Logs du conteneur** : Utiliser la commande `docker logs <nom_du_conteneur>` pour analyser les messages d'erreur ou avertissements. Cela fournit souvent des indices précieux.
* **Inspecter le conteneur** : La commande `docker inspect <nom_du_conteneur>` permet d’afficher des informations détaillées sur le conteneur (configuration, volumes, réseau, etc.). On y trouve des détails sur l'état du conteneur, les erreurs de démarrage, et la configuration réseau.
* **Etat du conteneur** : Utilise `docker ps -a` pour vérifier si le conteneur est en cours d'exécution, s'il est arrêté, ou s'il redémarre en boucle.

## Etape 2 - Approfondissement des recherches

### Valider la qualité des images

* **Reconstruire l'image** : Si l'image est corrompue ou mal construite, un nouveau build avec `docker build` peut être nécessaire. Regarde attentivement les étapes de construction pour identifier les erreurs potentielles.
* **Vérification de la version** : Assure-toi que l'image que tu utilises est à jour et que tu n’as pas des problèmes liés à des versions obsolètes ou incompatibles.

### Diagnostic des problèmes réseaux

* **Inspecter les réseaux Docker** : Si le problème est lié au réseau, tu peux inspecter les réseaux Docker avec `docker network ls` pour identifier des anomalies ou des conflits de configuration.
* **Inspecter le réseau d'un conteneur** : Utilise `docker inspect <nom_du_conteneur>` pour examiner les paramètres de réseau associés et vérifier que le conteneur est bien connecté au bon réseau.
* **Tester la connectivité** : Depuis l'intérieur du conteneur, tu peux tester la connectivité réseau avec des commandes telles que `curl`, `ping` ou `nslookup` en te connectant au shell du conteneur (`docker exec -it <nom_du_conteneur> bash`).

### Analyser les éléments de stockage

* **Vérification des volumes montés** : Un problème de volume peut provoquer des erreurs d'accès aux fichiers ou de permissions. Utilise `docker volume ls` pour voir quels volumes sont montés, et `docker inspect <nom_du_conteneur>` pour vérifier comment ils sont connectés au conteneur.
* **Permissions** : Assure-toi que les permissions des fichiers dans les volumes montés sont correctement configurées. Une erreur courante peut être que le conteneur n’a pas accès en écriture à un volume.

### Ressources systèmes et limitations

* **Surveillance des ressources** : Un conteneur peut ne pas fonctionner correctement en raison de limites sur l’utilisation du CPU, de la mémoire, ou du disque. Utilise `docker stats` pour surveiller les ressources utilisées par le conteneur.
* **Limites imposées** : Vérifie les limites de ressources appliquées au conteneur lors de son lancement (`docker run` ou configuration dans `docker-compose.yml`), comme les limites de mémoire ou de CPU.

### Vérifier l'état de santé du Docker Host

* **Docker Desktop** : Si tu utilises Docker Desktop, il offre des outils graphiques pour observer l’état des conteneurs, des volumes, et des réseaux.
* **Docker logs et journalisation système** : Si le problème est lié au démon Docker lui-même, tu peux consulter les logs du service Docker pour voir s'il y a des erreurs système (`journalctl -u docker` sur Linux).



