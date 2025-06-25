# Une machine virtuelle

## Qu'est-ce qu'une machine virtuelle ?

"Une machine virtuelle (VM) est un <mark style="color:orange;">logiciel</mark> qui <mark style="color:orange;">émule un ordinateur physique</mark>, permettant de faire fonctionner un système d'exploitation et des applications comme sur une machine réelle. Elle est gérée par un <mark style="color:orange;">hyperviseur</mark>, qui <mark style="color:orange;">alloue des ressources matérielles</mark> (processeur, mémoire, stockage) de la machine physique à la VM. <mark style="color:orange;">Chaque VM est totalement isolée</mark>, ce qui permet de les utiliser indépendamment les unes des autres <mark style="color:orange;">sans interférence</mark>. Les machines virtuelles sont couramment utilisées pour <mark style="color:orange;">tester des applications</mark>, <mark style="color:orange;">exécuter des systèmes d'exploitation différents sur une seule machine</mark>, ou <mark style="color:orange;">optimiser l'utilisation des ressources matérielles</mark>. Elles sont essentielles dans les environnements de virtualisation et de <mark style="color:orange;">cloud computing</mark>."

## Les concepts clés d'une machine virtuelle

Source: [VmWare](https://www.vmware.com/solutions/cloud-infrastructure/virtualization)

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td>Partitioning</td><td><ul><li>Exécuter différents systèmes d'exploitation au sein d'une seule machine physique.</li><li>Partager des ressources communes sur différentes machines virutelles.</li></ul></td><td></td></tr><tr><td>Isolation</td><td><ul><li>Assure l'isolation des pannes et de la sécurité au niveau du matériel.</li><li>Préserve les performances grâce à des contrôles avancés des ressources. </li></ul></td><td></td></tr><tr><td>Encapsulation</td><td><ul><li>Sauvegarde l'état complet d'une machine virtuelle dans des fichiers.</li><li>Déplacer ou copies une machine aussi facilement que des fichiers.</li></ul></td><td></td></tr><tr><td>Hardware Independence</td><td><ul><li>Provisionner ou migrer n'importe quelle machine virtuelle vers n'importe quel serveur physique.</li></ul></td><td></td></tr></tbody></table>

### Cycle de vie d'une machine virtuelle

Source: [GCP](https://cloud.google.com/compute/docs/instances/instance-life-cycle?hl=fr)

Le schéma suivant montre les transitions entre les différents états d'une VM :

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption><p>Source : <a href="https://cloud.google.com/compute/docs/instances/instance-life-cycle?hl=fr">GCP</a></p></figcaption></figure>

Une VM peut avoir l'un des états suivants :

* `PROVISIONING` : les ressources sont allouées à la VM. La VM n'est pas encore en cours d'exécution.
* `STAGING` : des ressources sont acquises, et la VM se prépare pour le premier démarrage.
* `RUNNING` : la VM démarre ou est en cours d'exécution.
* `STOPPING` : la VM est en cours d'arrêt. Vous avez demandé un arrêt ou un échec. Il s'agit d'un état temporaire, après lequel la VM passe à l'état `TERMINATED`.
* `REPAIRING` : la VM est en cours de réparation. La réparation a lieu lorsque la VM a rencontré une erreur interne ou parce que la machine sous-jacente est indisponible pour cause de maintenance. Durant cette période, la VM ne peut pas être utilisée. et elle ne vous est pas facturée. Les VM en réparation ne sont pas couvertes par le [contrat de niveau de service (SLA)](https://cloud.google.com/compute/sla?hl=fr). Si la réparation aboutit, la VM reprend l'un des états ci-dessus.
* `TERMINATED` : la VM est arrêtée. Vous avez arrêté la VM ou celle-ci a subi un échec. Vous pouvez [redémarrer](https://cloud.google.com/compute/docs/instances/stop-start-instance?hl=fr#starting_a_stopped_instance) ou [supprimer](https://cloud.google.com/compute/docs/instances/deleting-instance?hl=fr) la VM.
* `SUSPENDING` : la VM est en cours de suspension. Vous avez [suspendu](https://cloud.google.com/compute/docs/instances/suspend-resume-instance?hl=fr) la VM.
* `SUSPENDED` : la VM est suspendue. Vous pouvez la [réactiver](https://cloud.google.com/compute/docs/instances/suspend-resume-instance?hl=fr#resume) ou la [supprimer](https://cloud.google.com/compute/docs/instances/deleting-instance?hl=fr).

Note : c'est hyperviseur qui gère ce cycle de vie.
