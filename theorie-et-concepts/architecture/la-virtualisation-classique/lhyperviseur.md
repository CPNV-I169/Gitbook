---
description: >-
  Objectif : Montrer les principes de base de différentes architectures et
  expliquer les procédures, les architectures et les dépendances des systèmes de
  conteneurs.
---

# L'hyperviseur

## Un hyperviseur

### Rôle de l'hyperviseur

"Un hyperviseur est un <mark style="color:orange;">logiciel</mark> qui permet la création et la gestion de machines virtuelles (VM) sur un <mark style="color:orange;">hôte physique</mark>. Il <mark style="color:orange;">divise les ressources matérielles de l'hôte</mark>, comme le processeur, la mémoire et le stockage, et les distribue entre plusieurs VM, tout en assurant leur <mark style="color:orange;">isolation</mark>. L'hyperviseur gère également l'<mark style="color:orange;">exécution</mark> des VM, s'assurant qu'elles fonctionnent efficacement <mark style="color:orange;">sans interférer</mark> les unes avec les autres. Il existe deux types principaux d'hyperviseurs : les hyperviseurs de <mark style="color:orange;">type 1</mark>, qui s'exécutent directement sur le matériel, et les hyperviseurs de <mark style="color:orange;">type 2</mark>, qui fonctionnent au-dessus d'un système d'exploitation hôte. Le rôle principal de l'hyperviseur est de <mark style="color:orange;">maximiser l'utilisation des ressources matérielles</mark> et d'assurer la flexibilité, la scalabilité et la sécurité des environnements virtuels."

### Hyperviseur type I et II

Les hyperviseurs de type I et II se distinguent principalement par leur mode de fonctionnement et leur <mark style="color:orange;">interaction avec le matériel</mark>.

1. **Type I (Bare-Metal Hypervisor)** : Ce type d'hyperviseur fonctionne <mark style="color:orange;">directement sur le matériel physique de l'hôte</mark>, sans passer par un système d'exploitation intermédiaire. En raison de cette proximité avec le matériel, les hyperviseurs de type I offrent généralement de <mark style="color:orange;">meilleures performances</mark>, une plus grande efficacité et une sécurité renforcée. Ils sont couramment utilisés dans les environnements de serveurs et de <mark style="color:orange;">centres de données</mark>.
2. **Type II (Hosted Hypervisor)** : L'hyperviseur de type II s'exécute <mark style="color:orange;">au-dessus d'un système d'exploitation hôte</mark>, comme une application logicielle. Il est plus simple à installer et à utiliser, ce qui le rend populaire pour les tests, le développement, ou pour exécuter plusieurs systèmes d'exploitation sur des ordinateurs personnels. Cependant, il peut être moins performant que le type I en raison de la couche supplémentaire du système d'exploitation hôte.

Source: [AWS](https://aws.amazon.com/compare/the-difference-between-type-1-and-type-2-hypervisors/)

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption><p>Source : medium.com</p></figcaption></figure>

