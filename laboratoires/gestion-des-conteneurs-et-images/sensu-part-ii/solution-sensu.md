# Solution Sensu

## Step 01 - Installer Sensu Go - Solution

### Créer le réseau Sensu

* Lister les réseaux actuellements présents sur votre installation

```bash
docker network ls
```

* Question : Quel type de réseau avons-nous créé ?

Un réseau "bridge". Etant donné que nous n'avons pas spécifié le type, il s'agit du type par défaut. Ceci est validé par la documentation officielle :

### Créer un volume pour Sensu

* Liste les volumes existants

```bash
docker volume ls
```

### Construire et lancer le conteneur dédié au backend de Sensu

* Questions concenrant la commande "docker run":
  * Paramètre -d ?
    * \--detach : Run container in background and print container ID
    * [Official doc](https://docs.docker.com/reference/cli/docker/container/run/#detach)
  * Paramète --rm ?
    * Automatically remove the container and its associated anonymous volumes when it exits
    * [Official doc](https://docs.docker.com/reference/cli/docker/container/run/#rm)

### Création du schéma de l'infrastructure Sensu

* [Documentation officielle](https://docs.sensu.io/sensu-go/latest/operations/deploy-sensu/install-sensu/)

```markdown
cloud-architecture-diagram

direction right

// Define groups and nodes
Docker Host [icon: Host]{
  SensuCtl[icon: aws-command-line-interface]
  Browser[icon: firefox]
  Docker Network [icon: aws-public-subnet]{
      Sensu Network [icon: aws-private-subnet] {
        Sensu-Backend [icon: docker]{
          HTTP API[icon: api]
          WebSocket API[icon: socket-io]
          Web UI [icon: app]
          Embedded ETCD STORE[icon: network]
        }
        Backend-Data [icon: storage]
        Sensu-Agent [icon: docker]{
          Agent API[icon: api]
          Stats Listener[icon: azure-static-apps]
        }
    }
  }
}

// Define connections
SensuCtl > HTTP API: HTTP-S 8080-8080
Browser > Web UI : HTTP-S 3000-3000
SensuCtl > Agent API : TCP-UDP 3030-60804
Sensu-Agent > WebSocket API : WS 8081
Backend-Data - Sensu-Backend
```

<figure><img src="../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>
