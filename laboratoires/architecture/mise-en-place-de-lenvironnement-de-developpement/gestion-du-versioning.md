# Gestion du versioning

## Git - outil de gestion de version

"Git is a [free and open source](https://git-scm.com/about/free-and-open-source) distributed version control system designed to handle everything from small to very large projects with speed and efficiency."

[Télécharger](https://git-scm.com/)

* [ ] Prendre la version "Standalone Installer"
* [ ] Laisser tous les paramètres par défaut

### Tests d'acceptations

1. Lancer une nouvelle instance de cmder, et exécuter la commande suivante:

```bash
git --version
```

Résultat attendu

```bash
git version X.XX.X.windows.X
```

2. Se rendre dans un répertoire dédié pour le développement et exécuter la commande git init pour initaliser un nouveau dépôt

```bash
cd <pathToMyDevFolder>
git init
Initialized empty Git repository in C:/Users/Glassey Nicolas/MyDevs/I169/GitIntro/.git/
```

3. Lister le contenu du répertoire

```bash
ls -la
total 4
drwxr-xr-x 1 SC-C221-LP07+Glassey Nicolas 197121 0 Aug 17 16:48 ./
drwxr-xr-x 1 SC-C221-LP07+Glassey Nicolas 197121 0 Aug 17 16:48 ../
drwxr-xr-x 1 SC-C221-LP07+Glassey Nicolas 197121 0 Aug 17 16:48 .git/
```
