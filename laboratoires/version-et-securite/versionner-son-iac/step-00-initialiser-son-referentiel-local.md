# Step 00 - Initialiser son référentiel local

## Se positionner au sein de notre projet (dans l'exemple "CustomNginx")

```bash
pwd
```

```
<yourPath>\CustomNginx
```

## Initialiser git

```bash
git init
```

```
Initialized empty Git repository in <yourPath>/CustomNginx/.git/
```

* Observer le répertoire caché ".git" (Note : sous Linux, un répertoire débutant par un point signifie qu'il est caché)

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption><p>Résultat via l'explorateur de Windows</p></figcaption></figure>

```bash
ls -la
```

```
total 9
drwxr-xr-x 1 SC-C221-LP07+Glassey Nicolas 197121   0 Aug 25 17:31 ./
drwxr-xr-x 1 SC-C221-LP07+Glassey Nicolas 197121   0 Aug 24 10:18 ../
drwxr-xr-x 1 SC-C221-LP07+Glassey Nicolas 197121   0 Aug 25 17:29 .git/
-rw-r--r-- 1 SC-C221-LP07+Glassey Nicolas 197121 145 Aug 25 12:37 Dockerfile
drwxr-xr-x 1 SC-C221-LP07+Glassey Nicolas 197121   0 Aug 25 12:12 html/
```

## Ajouter un Readme

* Créer le fichier README a la racine de votre projet et ajouter le contenu livré ci-dessous (en le mettant à jour)

```
touch README.md
```

````markdown
# Foobar

Foobar is a Python library for dealing with word pluralization.

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install foobar.

```bash
pip install foobar
```

## Usage

```python
import foobar

# returns 'words'
foobar.pluralize('word')

# returns 'geese'
foobar.pluralize('goose')

# returns 'phenomenon'
foobar.singularize('phenomena')
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)
````



{% hint style="info" %}
Pour favoriser la collaboration, votre README doit aider les futurs collaborateurs à vous rejoindre. Soigner la mise à jour de ce fichier !
{% endhint %}

* Intégrer le README à votre dépôt local

```bash
git add README
```

```bash
git commit -m "chore: add readme"
```

## Exclusion des fichiers et répertoires

* Ajouter un .gitignore pour éviter d'intégrer des données qui ne doivent pas être versionnées

```bash
touch .gitignore
```

* Ajouter le contenu dans le gitignore ([source](https://github.com/atlassian/docker/blob/master/.gitignore))

```git
# Docker project generated files to ignore
#  if you want to ignore files created by your editor/tools,
#  please consider a global .gitignore https://help.github.com/articles/ignoring-files
.vagrant*
bin
docker/docker
.*.swp
a.out
*.orig
build_src
.flymake*
.idea
.DS_Store
docs/_build
docs/_static
docs/_templates
.gopath/
.dotcloud
*.test
bundles/
.hg/
.git/
vendor/pkg/
pyenv
Vagrantfile
```

* Intégrer le gitignore à votre dépôt local

{% hint style="info" %}
Ajouter le gitignore dès le début du projet est une bonne pratique. Un ajout ultérieure risquerait de demander de la maintenance:

* un fichier/répertoire qui aurait déjà été ajouté ne va pas être ignoré sans le supprimer du [cache de git](https://git-scm.com/docs/git-rm)
{% endhint %}

```bash
git add .gitignore
```

{% code overflow="wrap" %}
```
warning: in the working copy of '.gitignore', LF will be replaced by CRLF the next time Git touches it
```
{% endcode %}

```bash
git commit -m "chore: add gitignore"
```

```
[main (root-commit) b921fb1] chore: add gitignore
 1 file changed, 25 insertions(+)
 create mode 100644 .gitignore
```

## Intégrer les fichiers du projet

* Ajouter le contenu de notre projet au VCS

```bash
git add .
```

```
warning: in the working copy of 'html/login/fonts/font-awesome-4.7.0/HELP-US-OUT.txt', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'html/login/fonts/font-awesome-4.7.0/css/font-awesome.css', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'html/login/fonts/font-awesome-4.7.0/css/font-awesome.min.css', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'html/login/fonts/font-awesome-4.7.0/fonts/fontawesome-webfont.svg', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'html/login/fonts/font-awesome-4.7.0/less/animated.less', LF will be replaced by CRLF the next time Git touches it
warning: in the working copy of 'html/login/fonts/font-awesome-4.7.0/less/bordered-pulled.less', LF will be replaced by CRLF the next time Git touches it
[...]
warning: in the working copy of 'html/login/fonts/font-awesome-4.7.0/less/fixed-width.less', LF will be replaced by CRLF the next time Git touches it
```

* Vérifier que le contenu désiré a bien été détecté

```bash
git status
```

```
new file:   Dockerfile
new file:   html/index.html
new file:   html/login/css/main.css
[...]
new file:   html/login/vendor/select2/select2.min.css
new file:   html/login/vendor/select2/select2.min.js
new file:   html/login/vendor/tilt/tilt.jquery.min.js
```

{% hint style="info" %}
On observe le contenu HTML tout comme le fichier "Dockerfile"
{% endhint %}

* Créer une version de ces fichiers

```bash
git commit -m "feat: nginx with login form"
```

```
//the list of files integrated
```

* Vérifier que le dépôt local est à jour

```bash
git status
```

```
On branch main
nothing to commit, working tree clean
```







