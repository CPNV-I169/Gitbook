# Topologie réseau

Pour obtenir les adresses IP internes de tous les conteneurs qui appartiennent à un même réseau Docker, vous pouvez suivre les étapes ci-dessous :

#### 1. **Lister les Conteneurs sur le Réseau**

Tout d'abord, vous devez identifier le nom du réseau auquel vos conteneurs sont connectés. Vous pouvez lister tous les réseaux Docker avec la commande suivante :

```bash
docker network ls
```

Cette commande retournera une liste de réseaux disponibles. Identifiez le réseau qui vous intéresse.

#### 2. **Inspecter le Réseau**

Une fois que vous avez identifié le réseau, vous pouvez inspecter ce réseau pour obtenir des informations détaillées sur tous les conteneurs connectés, y compris leurs adresses IP internes. Utilisez la commande suivante en remplaçant `<network_name>` par le nom de votre réseau :

```bash
docker network inspect <network_name>
```

Cette commande retourne un JSON contenant des informations sur le réseau, y compris les conteneurs connectés et leurs adresses IP internes.

#### 3. **Filtrer les Adresses IP**

Dans la sortie JSON de la commande `docker network inspect`, vous trouverez une section appelée `"Containers"` qui contient des informations sur tous les conteneurs connectés au réseau. Chaque conteneur aura une entrée contenant son `Id`, `Name`, et `IPv4Address` (ou `IPv6Address` si applicable). Vous pouvez filtrer cette sortie pour extraire les adresses IP.

Par exemple, pour extraire juste les adresses IP avec un outil comme `jq`, vous pouvez utiliser :

```bash
docker network inspect <yourNetwork> | jq -r ".[0].Containers[] | \"\(.Name) \(.IPv4Address)""
```

| Commande/Paramètre     | Explications                                                                                                                                                                       |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| docker                 | appelle le client docker                                                                                                                                                           |
| network                | librairie docker spécialisée pour le réseau                                                                                                                                        |
| inspect                | option de "network" pour faire de l'analyse                                                                                                                                        |
| \<yourNetwork>         | à remplacer par le nom du réseau que vous désirez analyser (docker network ls)                                                                                                     |
| \|                     | <p>"pipe" permet de transmettre le résultat de la commande précédente pour la suite de la commande.<br><br>Dans notre cas, docker network livrera un JSON décrivant le réseau.</p> |
| jq                     | Utilitaire "json query" permettant de manipuler du contenu json.                                                                                                                   |
| -r  (--raw-output)     | Permet d'afficher le résultat en ligne et non en format JSON.                                                                                                                      |
| \[0].Containers\[]     | Extrait tous les éléments de second niveau (le premier niveau étant 0), dont le nom est "Containers".                                                                              |
| (.Name) (.IPv4Address) | Extrait uniquement les attributs "name" et "ipv4address"                                                                                                                           |

\
[Documentation officielle de jq](./#id-1.-lister-les-conteneurs-sur-le-reseau)
