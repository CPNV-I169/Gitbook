# Step 02 - Installer Sensu Go CLI

* Récupérer l'archive contenant l'exécutable pour le CLI de Sensu



{% hint style="info" %}
A partir de cette étape, les commandes présentées sont réalisées avec PowerShell
{% endhint %}

```powershell
Invoke-WebRequest `
-Uri https://s3-us-west-2.amazonaws.com/sensu.io/sensu-go/6.11.0/sensu-go_6.11.0_windows_amd64.zip  `
-OutFile sensu-go_6.11.0_windows_amd64.zip
```

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption><p>Capture d'écran durant le téléchargement de l'archive</p></figcaption></figure>

{% hint style="info" %}
A partir de cette étape, on quitte PowerShell
{% endhint %}

* Décompresser l'archive

```bash
unzip sensu-go_6.11.0_windows_amd64.zip
```

```
Archive:  sensu-go_6.11.0_windows_amd64.zip
  inflating: CHANGELOG-6.md
  inflating: LICENSE
  inflating: README.md
  inflating: sensu-agent.exe
  inflating: sensuctl.exe
```

* Configurer le client

```bash
sensuctl.exe configure -n ^
--url http://127.0.0.1:8080 ^
--username admin ^
--password "P@ssw0rd!" ^
--namespace default
```

* Valider l'état du cluster Sensu

```bash
sensuctl cluster health
```

```
=== Etcd Cluster ID: 64fe15c34d6aa880
         ID           Name     Error   Healthy
─────────────────── ───────── ─────── ──────────
  8cbb58cccef82cbe   default           true
```

* Demander l'identifiant de notre cluster

```
sensuctl.exe cluster id
```

```
sensu cluster id: "65ea6d05-65d7-4f40-ac72-5a44f001885f"
```

## Mettre à jour le schéma de l'infrastructure

* Ajouter le client ainsi que les ports et les protocoles utilisés
