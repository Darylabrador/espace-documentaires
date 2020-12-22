# Design pattern : Visitor

Visiteur est un modèle de conception comportementale qui vous permet de séparer les algorithmes des objets sur lesquels ils opèrent.

### Ressources :

- https://refactoring.guru/design-patterns/visitor

### Problématiques :

Imaginez que votre équipe développe une application qui fonctionne avec des informations géographiques structurées comme un graphe colossal. Chaque nœud du graphique peut représenter une entité complexe telle qu'une ville, mais également des éléments plus granulaires tels que des industries, des sites touristiques, etc. Les nœuds sont connectés aux autres s'il existe une route entre les objets réels qu'ils représentent. Sous le capot, chaque type de nœud est représenté par sa propre classe, tandis que chaque nœud spécifique est un objet.

À un moment donné, vous avez une tâche pour implémenter l'exportation du graphique au format XML. Au début, le travail semblait assez simple. Vous avez prévu d'ajouter une méthode d'exportation à chaque classe de nœuds, puis de tirer parti de la récursivité pour parcourir chaque nœud du graphique, en exécutant la méthode d'exportation. La solution était simple et élégante: grâce au polymorphisme, vous n’aviez pas couplé le code qui appelait la méthode d’exportation à des classes concrètes de nœuds.

Malheureusement, l'architecte système a refusé de vous autoriser à modifier les classes de nœuds existantes. Il a dit que le code était déjà en production et qu'il ne voulait pas risquer de le casser à cause d'un bug potentiel dans vos modifications.

De plus, il s'est demandé s'il était judicieux d'avoir le code d'exportation XML dans les classes de nœuds. Le travail principal de ces classes était de travailler avec des géodonnées. Le comportement d'exportation XML y paraîtrait étranger.

Il y avait une autre raison au refus. Il était fort probable qu'après la mise en œuvre de cette fonctionnalité, quelqu'un du service marketing vous demande de fournir la possibilité d'exporter dans un format différent, ou de demander d'autres choses étranges. Cela vous obligerait à changer à nouveau ces classes précieuses et fragiles.

### Solution :

Le modèle Visiteur vous suggère de placer le nouveau comportement dans une classe distincte appelée visiteur, au lieu d'essayer de l'intégrer dans des classes existantes. L’objet d’origine qui devait exécuter le comportement est maintenant transmis à l’une des méthodes du visiteur en tant qu’argument, permettant à la méthode d’accéder à toutes les données nécessaires contenues dans l’objet.

Pour plus de détails <a href="https://refactoring.guru/design-patterns/visitor"> regardez l'espace "solution" </a>


### Quand est ce qu'il faut l'appliquer ?

- Utilisez le Visiteur lorsque vous devez effectuer une opération sur tous les éléments d'une structure d'objet complexe (par exemple, une arborescence d'objets).

- Utilisez le Visiteur pour nettoyer la logique métier des comportements auxiliaires.

- Utilisez le modèle lorsqu'un comportement n'a de sens que dans certaines classes d'une hiérarchie de classes, mais pas dans d'autres.

### Comment l'implémenter ?

- Déclarez l'interface visiteur avec un ensemble de méthodes de «visite», une pour chaque classe d'élément concrète qui existe dans le programme.

- Déclarez l'interface de l'élément. Si vous travaillez avec une hiérarchie de classes d'éléments existante, ajoutez la méthode abstraite "acceptation" à la classe de base de la hiérarchie. Cette méthode doit accepter un objet visiteur comme argument.

- Implémentez les méthodes d'acceptation dans toutes les classes d'éléments concrets. Ces méthodes doivent simplement rediriger l'appel vers une méthode de visite sur l'objet visiteur entrant qui correspond à la classe de l'élément courant.

- Les classes d'éléments ne doivent fonctionner qu'avec les visiteurs via l'interface visiteur. Les visiteurs, cependant, doivent être conscients de toutes les classes d'éléments concrets, référencées en tant que types de paramètres des méthodes de visite.

- Pour chaque comportement qui ne peut pas être implémenté dans la hiérarchie des éléments, créez une nouvelle classe de visiteur concrète et implémentez toutes les méthodes de visite. Vous pouvez rencontrer une situation où le visiteur aura besoin d'accéder à certains membres privés de la classe d'élément. Dans ce cas, vous pouvez soit rendre ces champs ou méthodes publics, en violant l'encapsulation de l'élément, soit imbriquer la classe de visiteur dans la classe d'élément. Ce dernier n’est possible que si vous avez la chance de travailler avec un langage de programmation prenant en charge les classes imbriquées.

- Le client doit créer des objets visiteurs et les passer en éléments via des méthodes «d'acceptation».

### Avantages :

- Principe ouvert / fermé. Vous pouvez introduire un nouveau comportement qui peut fonctionner avec des objets de différentes classes sans changer ces classes.
- Principe de responsabilité unique. Vous pouvez déplacer plusieurs versions du même comportement dans la même classe.
- Un objet visiteur peut accumuler des informations utiles tout en travaillant avec divers objets. Cela peut être pratique lorsque vous souhaitez parcourir une structure d'objet complexe, telle qu'une arborescence d'objets, et appliquer le visiteur à chaque objet de cette structure.

### Inconvénients :

- Vous devez mettre à jour tous les visiteurs chaque fois qu'une classe est ajoutée ou supprimée de la hiérarchie des éléments.
- Les visiteurs peuvent ne pas avoir accès aux champs privés et aux méthodes des éléments avec lesquels ils sont censés travailler.