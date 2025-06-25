# Docker Engine

## Préparer votre environnement avant l'installation (pré-requis)

[Source](https://docs.docker.com/desktop/install/windows-install/#system-requirements)

* [ ] [Installer WSL](https://learn.microsoft.com/en-us/windows/wsl/install)

```powershell
ps > wsl --install debian
Installing: Virtual Machine Platform
Virtual Machine Platform has been installed.
Installing: Windows Subsystem for Linux
Windows Subsystem for Linux has been installed.
Installing: Windows Subsystem for Linux
Windows Subsystem for Linux has been installed.
Installing: Debian
Ubuntu has been installed.
The requested operation is successful. Changes will not be effective until the system is rebooted.
```

* [ ] Redémarrer votre système

```
run shutdown -r -t 00
```

### Tests d'acceptation

1. Lancer wsl. Lors du premier lancement il va vous être demandé de créer un utilisateur pour votre distribution Linux

```
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: admin
New password:
Retype new password:
passwd: password updated successfully
Installation successful!
admin@SC-C221-LP07:~$
```

## Installer le Docker Engine

[Télécharger](https://docs.docker.com/engine/install/)

* [ ] Après l'installation, lancer le docker destop (c'est la seule manière pour lancer le docker engine sous windows)
* [ ] Se connecter (ou créer un compte Docker)
* [ ] Répondre au "welcome survey"
*   [ ] En bas à droite de l'écran d'accueil de Docker Desktop, il vous sera peut-être mentionné de faire une mise à jour. Faites-la !\


    <figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>


* [ ] Vérifier que votre système est à jour

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

* [ ] Observer le statut de l'Engine

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

* [ ] Exécuter votre première commande via le cli de Docker pour valider l'installation (il s'agit de lister tous les conteneurs actuellement présents sur votre machine. Il est donc normal que le résultat, excepté les entêtes des colonnes, soit vide).

```docker
docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
