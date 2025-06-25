# Visual Studio Code

## Visual Studio Code - Editeur de code

"Visual Studio Code is a lightweight but powerful source code editor which runs on your desktop and is available for Windows, macOS and Linux. It comes with built-in support for JavaScript, TypeScript and Node.js and has a rich ecosystem of extensions for other languages and runtimes (such as C++, C#, Java, Python, PHP, Go, .NET)."

[Télécharger](https://code.visualstudio.com/download)

* [ ] Installer la version pour Windows
* [ ] Ajouter l'extension pour [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
* [ ] Ajouter l'extension pour le [MarkDown](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
* [ ] Ajouter l'extension pour l'impression [Markdown to pdf](https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf)



Option - configurer cmder comme terminal par défaut dans Visual Studio Code

* [ ] Ouvrir Visual Studio Code
* [ ] Appuyer sur "ctl + shift + p"

<figure><img src="../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

* [ ] Saisir "open user settings" et choisir le "user settings" et ajouter ce contenu

{% hint style="danger" %}
Respecter bien la structure du json existant !\
\
Mettre à jour le chemin pointant vers votre installation "\<PathToYourCmderInstallation>"
{% endhint %}

```
     "terminal.integrated.profiles.windows": {
  "Cmder": {
    "path": "${env:windir}\\System32\\cmd.exe",
    "args": ["/k", "<PathToYourCmderInstallation>\\cmder\\vendor\\init.bat"]
  }
},
"terminal.integrated.defaultProfile.windows": "Cmder",
```

* [ ] Tester l'insallation en ouvrant un terminal. Voici le résultat attendu:

<figure><img src="../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

