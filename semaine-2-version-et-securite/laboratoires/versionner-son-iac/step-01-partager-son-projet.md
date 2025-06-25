# Step 01 - Partager son projet

### Ouvrir un compte Github

* [Lien sur le site de github](https://github.com/signup?ref_cta=Sign+up\&ref_loc=header+logged+out\&ref_page=%2F\&source=header-home)

{% hint style="info" %}
Utiliser votre email professionnel (soit comme adresse prinicpale, [soit comme secondaire](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/adding-an-email-address-to-your-github-account))
{% endhint %}

### Créer un projet dédié à notre projet

* [Lien sur le site de github](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories#create-a-repository)

{% hint style="info" %}
Veillez à bien créer un projet:

* publique
* vide (ni Readme, ni gitignore car nous les avons déjà créés à l'étape précédente)
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (49).png" alt=""><figcaption><p>Aperçu de l'écran de création du dépôt dans Github</p></figcaption></figure>

## Lier vos deux référentiels

* Référence le projet distant dans les "remote" du projet local

```bash
git remote add origin "<url de votre référentiel distant>"
```

* Vérifier que le "remote" a bien été intégré

```bash
git remote -v
```

```bash
origin  https://github.com/<votre Url>/CustomNginx.git (fetch)
origin  https://github.com/<votre Url>/CustomNginx.git (push)
```

## Publier le code

* Vérifier que le nommage de votre branche principale respect bien les normes Github. Votre branche doit être "main" et non "master"

```bash
git branch
```

```
* master  //ceci doit être renommer
```

* Si besoin, renommer la branche de votre dépôt local (en restant sur la branche à renommer)

```bash
git branch -m main
```

* Réaliser votre premier "push"

```bash
git push --set-upstream origin main
```

```
Enumerating objects: 136, done.
Counting objects: 100% (136/136), done.
Delta compression using up to 12 threads
Compressing objects: 100% (130/130), done.
Writing objects: 100% (136/136), 4.19 MiB | 3.12 MiB/s, done.
Total 136 (delta 9), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (9/9), done.
To https://github.com/CPVN-I169/CustomNginx.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

* Vérifier que le contenu est bien disponible sur votre dépôt

<figure><img src="../../../.gitbook/assets/image (50).png" alt=""><figcaption><p>Aperçu sur Github de résultat du premier "push"</p></figcaption></figure>

## Publier le lien de votre dépôt

{% embed url="https://eduvaud.sharepoint.com/:x:/r/sites/CPNV_22-26_SI-CMi_a_Teams-I169/Documents%20partages/I169/CustomNginx.xlsx?d=w3769473cd5de4edbb1672dca97e9a9cb&csf=1&web=1&e=EK4vJg" %}
Lien pointant vers le fichier permettant d'annoncer votre dépôt
{% endembed %}
