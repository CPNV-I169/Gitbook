# Devops et les outils nécessaires

## Les outils de devops

Dans ce module nous appréhendons les techniques de déploiement de services, à l'aide de conteneurs. Il est difficile de ne pas faire une parenthèse sur un terme et des pratiques associées de plus en plus courantes, le devops.

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption><p>Source : <a href="https://www.dynatrace.com/news/blog/what-is-devops/">dynatrace.com</a></p></figcaption></figure>

"Le DevOps est une <mark style="color:orange;">approche</mark> qui combine le <mark style="color:orange;">développement logiciel (Dev)</mark> et les <mark style="color:orange;">opérations informatiques (Ops)</mark> pour améliorer la collaboration, l'efficacité et la qualité du développement et de la livraison des applications. Il vise à <mark style="color:orange;">automatiser et à intégrer les processus entre les équipes</mark> de développement et d'opérations, facilitant ainsi des <mark style="color:orange;">déploiements plus fréquents</mark> et plus fiables. DevOps favorise une culture de collaboration continue, d'amélioration et de partage des responsabilités tout au long du cycle de vie du logiciel."

## Les différents phases de projets et leur outils

### Build

Phase durant laquelle les équipes vont <mark style="color:orange;">provisionner</mark> les environnements. On parle ici de la partie infrastructure nécessaire au bon fonctionnement de la solution qui sera ensuite déployée par-dessus.

A cette étape, il est essentiel d'avoir une approche IaC (<mark style="color:orange;">Infrastructure As Code</mark>). Ainsi vous favorisez une approche agile, y compris sur l'infrastructure. La configuration de votre infrastructure est ainsi <mark style="color:orange;">documentée, versionnée et facilement maintenable</mark>.

L'utilisation de scripts facilitent également la mise en place d'environnements identiques pour les différentes phases du développement. Cela réduit les efforts pour le passage en production étant donné que le produit aura été développé sur un environnement similaire à celui de la production.

### Source control and collaborative coding

Phase durant laquelle les équipes produisent la solution logicielle. Dans ce module nous utiliserons les outils de versionning pour gérer les versions de nos scripts de déploiement, mais nous de développerons pas d'applicatif.

### Les différentes phases de développement

Il existe de nombreuses étapes spécifiques à l'approche devops. Ici ne sont présentées que les deux étapes spécifique au provisionnement des l'infrastructure.

Source: [Atlassian - devops tools](https://www.atlassian.com/devops/devops-tools)
