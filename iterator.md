# Design pattern : Iterator

Iterator est un modèle de conception comportementale qui vous permet de parcourir les éléments d'une collection sans exposer sa représentation sous-jacente (liste, pile, arbre, etc.).

### Ressources :

- https://refactoring.guru/design-patterns/iterator

### Problématiques :

Les collections sont l'un des types de données les plus utilisés en programmation. Néanmoins, une collection n'est qu'un conteneur pour un groupe d'objets. La plupart des collections stockent leurs éléments dans des listes simples. Cependant, certains d'entre eux sont basés sur des piles, des arbres, des graphiques et d'autres structures de données complexes. Mais quelle que soit la structure d'une collection, elle doit fournir un moyen d'accéder à ses éléments afin que d'autres codes puissent utiliser ces éléments. Il devrait y avoir un moyen de parcourir chaque élément de la collection sans accéder aux mêmes éléments encore et encore.

Cela peut sembler un travail facile si vous avez une collection basée sur une liste. Vous bouclez simplement sur tous les éléments. Mais comment parcourir séquentiellement des éléments d'une structure de données complexe, telle qu'un arbre? Par exemple, un jour, vous pourriez être très bien avec la traversée en profondeur d'un arbre. Pourtant, le lendemain, vous pourriez avoir besoin d'une traversée en largeur d'abord. Et la semaine prochaine, vous pourriez avoir besoin de quelque chose d'autre, comme un accès aléatoire aux éléments de l'arborescence.

L'ajout de plus en plus d'algorithmes de parcours à la collection brouille progressivement sa responsabilité première, qui est le stockage efficace des données. De plus, certains algorithmes peuvent être adaptés à une application spécifique, il serait donc étrange de les inclure dans une classe de collection générique. D'un autre côté, le code client qui est censé fonctionner avec diverses collections peut même ne pas se soucier de la façon dont ils stockent leurs éléments. Cependant, étant donné que les collections fournissent toutes différentes manières d'accéder à leurs éléments, vous n'avez pas d'autre choix que de coupler votre code aux classes de collection spécifiques.

### Solution :

L'idée principale du modèle Iterator est d'extraire le comportement de traversée d'une collection dans un objet séparé appelé itérateur.

En plus d'implémenter l'algorithme lui-même, un objet itérateur encapsule tous les détails de traversée, tels que la position actuelle et le nombre d'éléments restants jusqu'à la fin. De ce fait, plusieurs itérateurs peuvent parcourir la même collection en même temps, indépendamment les uns des autres. Habituellement, les itérateurs fournissent une méthode principale pour récupérer les éléments de la collection. Le client peut continuer à exécuter cette méthode jusqu'à ce qu'elle ne renvoie rien, ce qui signifie que l'itérateur a traversé tous les éléments.

Tous les itérateurs doivent implémenter la même interface. Cela rend le code client compatible avec n'importe quel type de collection ou n'importe quel algorithme de traversée tant qu'il existe un itérateur approprié. Si vous avez besoin d'un moyen spécial pour parcourir une collection, vous créez simplement une nouvelle classe d'itérateur, sans avoir à modifier la collection ou le client.


### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Iterator lorsque votre collection a une structure de données complexe sous le capot, mais que vous souhaitez cacher sa complexité aux clients (pour des raisons de commodité ou de sécurité).
- Utilisez le modèle pour réduire la duplication du code de parcours dans votre application.
- Utilisez l'itérateur lorsque vous souhaitez que votre code puisse traverser différentes structures de données ou lorsque les types de ces structures sont inconnus au préalable.

### Comment l'implémenter ?

- Déclarez l'interface de l'itérateur. À tout le moins, il doit avoir une méthode pour récupérer l'élément suivant d'une collection. Mais pour des raisons de commodité, vous pouvez ajouter quelques autres méthodes, telles que la récupération de l'élément précédent, le suivi de la position actuelle et la vérification de la fin de l'itération.

- Déclarez l'interface de collection et décrivez une méthode pour récupérer les itérateurs. Le type de retour doit être égal à celui de l'interface de l'itérateur. Vous pouvez déclarer des méthodes similaires si vous prévoyez d'avoir plusieurs groupes distincts d'itérateurs.

- Implémentez des classes d'itérateurs concrètes pour les collections que vous souhaitez traverser avec des itérateurs. Un objet itérateur doit être lié à une seule instance de collection. Habituellement, ce lien est établi via le constructeur de l’itérateur.

- Implémentez l'interface de collection dans vos classes de collection. L'idée principale est de fournir au client un raccourci pour créer des itérateurs, adapté à une classe de collection particulière. L’objet de collection doit se transmettre au constructeur de l’itérateur pour établir un lien entre eux.

- Passez en revue le code client pour remplacer tout le code de traversée de la collection par l'utilisation d'itérateurs. Le client récupère un nouvel objet itérateur à chaque fois qu'il doit parcourir les éléments de la collection.

### Avantages :

- Principe de responsabilité unique. Vous pouvez nettoyer le code client et les collections en extrayant des algorithmes de parcours volumineux dans des classes distinctes.
- Principe ouvert / fermé. Vous pouvez implémenter de nouveaux types de collections et d'itérateurs et les transmettre au code existant sans rien casser.
- Vous pouvez parcourir la même collection en parallèle car chaque objet itérateur contient son propre état d'itération.
- Pour la même raison, vous pouvez retarder une itération et la poursuivre si nécessaire.

### Inconvénients :

- L'application du modèle peut être excessive si votre application ne fonctionne qu'avec des collections simples.
- L'utilisation d'un itérateur peut être moins efficace que de parcourir directement les éléments de certaines collections spécialisées.