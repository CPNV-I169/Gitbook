# Step 00 - Objectif du laboratoire

## Intentions pédagogiques

Dans ce laboratoire, nous allons déployer une infrastructure "réelle", en se basant sur un produit du nom de Sensu.

Cela permettra de nous entraîner au déployement d'une solution que vous pourriez rencontrer par exemple en stage. Les notions vues théorie telles que les namespaces, les réseaux seront mises en applications.

Pour bien visualiser l'instrastructure que nous allons mettre en place, nous entraînerons également le dessin d'infrastructure informatique.

## Objectifs opérationnels

Déployer en local, en suivant la documentation, la solution Sensu qui comporte:

* [ ] Un réseau dédié pour améliorer l'isolation ([Docker newtork](https://docs.docker.com/engine/network/)).
* [ ] Un backend contenant la logique métier du produit ainsi que la persistence de données ([Docker volumes](https://docs.docker.com/engine/storage/volumes/) ).
* [ ] Un agent qui récollte les métriques des clients à monitorer.
* [ ] Un client nous permettant de piloter Sensu et mettre en place un cluster Sensu en ligne de commande.
* [ ] Monitorer sa propre machine et voir apparaître les métriques de bases dans la console web de Sensu.

