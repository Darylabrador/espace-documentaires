# Design pattern : Strategy

La stratégie est un modèle de conception comportementale qui vous permet de définir une famille d'algorithmes, de placer chacun d'eux dans une classe distincte et de rendre leurs objets interchangeables.

### Ressources :

- https://refactoring.guru/design-patterns/strategy

### Problématiques :

Un jour, vous avez décidé de créer une application de navigation pour les voyageurs occasionnels. L'application était centrée sur une belle carte qui aidait les utilisateurs à s'orienter rapidement dans n'importe quelle ville. L'une des fonctionnalités les plus demandées pour l'application était la planification d'itinéraire automatique. Un utilisateur doit pouvoir entrer une adresse et voir l'itinéraire le plus rapide vers cette destination affiché sur la carte.

La première version de l'application ne pouvait construire les itinéraires que sur des routes. Les gens qui voyageaient en voiture débordaient de joie. Mais apparemment, tout le monde n'aime pas conduire pendant ses vacances. Donc, avec la prochaine mise à jour, vous avez ajouté une option pour créer des itinéraires à pied. Juste après cela, vous avez ajouté une autre option pour permettre aux gens d'utiliser les transports en commun sur leurs itinéraires.

Cependant, ce n’était que le début. Plus tard, vous avez prévu d'ajouter la création d'itinéraire pour les cyclistes. Et même plus tard, une autre option pour créer des itinéraires à travers toutes les attractions touristiques d'une ville. Si d'un point de vue commercial, l'application a été un succès, la partie technique vous a causé de nombreux maux de tête. Chaque fois que vous avez ajouté un nouvel algorithme de routage, la classe principale du navigateur a doublé de taille. À un moment donné, la bête est devenue trop difficile à entretenir.

Toute modification de l'un des algorithmes, qu'il s'agisse d'une simple correction de bogue ou d'un léger ajustement du score de la rue, affectait toute la classe, augmentant le risque de créer une erreur dans un code déjà fonctionnel. De plus, le travail d'équipe est devenu inefficace. Vos coéquipiers, qui avaient été embauchés juste après la sortie réussie, se plaignent de passer trop de temps à résoudre les conflits de fusion. L'implémentation d'une nouvelle fonctionnalité vous oblige à changer la même classe énorme, en conflit avec le code produit par d'autres personnes.

### Solution :

Le modèle de stratégie suggère que vous preniez une classe qui fait quelque chose de spécifique de nombreuses manières différentes et que vous extrayiez tous ces algorithmes dans des classes distinctes appelées stratégies. La classe d'origine, appelée context, doit avoir un champ pour stocker une référence à l'une des stratégies. Le contexte délègue le travail à un objet de stratégie lié au lieu de l'exécuter seul.

Le contexte n’est pas responsable de la sélection d’un algorithme approprié pour le travail. Au lieu de cela, le client transmet la stratégie souhaitée au contexte. En fait, le contexte en sait peu sur les stratégies. Il fonctionne avec toutes les stratégies via la même interface générique, qui n'expose qu'une seule méthode pour déclencher l'algorithme encapsulé dans la stratégie sélectionnée.

De cette façon, le contexte devient indépendant des stratégies concrètes, vous pouvez donc ajouter de nouveaux algorithmes ou modifier ceux existants sans changer le code du contexte ou d'autres stratégies. Dans notre application de navigation, chaque algorithme de routage peut être extrait dans sa propre classe avec une seule méthode buildRoute. La méthode accepte une origine et une destination et renvoie une collection des points de contrôle de l'itinéraire.

Même si elle reçoit les mêmes arguments, chaque classe de routage peut créer une route différente, la classe de navigateur principale ne se soucie pas vraiment de l’algorithme sélectionné, car sa tâche principale est de rendre un ensemble de points de contrôle sur la carte. La classe dispose d'une méthode pour changer la stratégie de routage active, de sorte que ses clients, tels que les boutons de l'interface utilisateur, peuvent remplacer le comportement de routage actuellement sélectionné par un autre.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle de stratégie lorsque vous souhaitez utiliser différentes variantes d'un algorithme dans un objet et pouvoir passer d'un algorithme à un autre pendant l'exécution.
- Utilisez la stratégie lorsque vous avez de nombreuses classes similaires qui ne diffèrent que par la manière dont elles exécutent certains comportements.
- Utilisez le modèle pour isoler la logique métier d'une classe des détails d'implémentation d'algorithmes qui peuvent ne pas être aussi importants dans le contexte de cette logique.
- Utilisez le modèle lorsque votre classe a un opérateur conditionnel massif qui bascule entre différentes variantes du même algorithme.

### Comment l'implémenter ?

- Dans la classe de contexte, identifiez un algorithme sujet à des changements fréquents. Il peut également s'agir d'un conditionnel massif qui sélectionne et exécute une variante du même algorithme au moment de l'exécution.

- Déclarez l'interface de stratégie commune à toutes les variantes de l'algorithme.

- Un par un, extrayez tous les algorithmes dans leurs propres classes. Ils devraient tous mettre en œuvre l'interface stratégique.

- Dans la classe de contexte, ajoutez un champ pour stocker une référence à un objet de stratégie. Fournissez un setter pour remplacer les valeurs de ce champ. Le contexte doit fonctionner avec l'objet de stratégie uniquement via l'interface de stratégie. Le contexte peut définir une interface qui permet à la stratégie d'accéder à ses données.

- Les clients du contexte doivent l'associer à une stratégie appropriée qui correspond à la façon dont ils s'attendent à ce que le contexte exécute son travail principal.

### Avantages :

- Vous pouvez permuter les algorithmes utilisés à l'intérieur d'un objet au moment de l'exécution.
- Vous pouvez isoler les détails d'implémentation d'un algorithme du code qui l'utilise.
- Vous pouvez remplacer l'héritage par la composition.
- Principe ouvert / fermé. Vous pouvez introduire de nouvelles stratégies sans avoir à changer de contexte.

### Inconvénients :

- Si vous ne disposez que de quelques algorithmes et qu'ils changent rarement, il n'y a aucune raison de compliquer le programme avec de nouvelles classes et interfaces qui accompagnent le modèle.
- Les clients doivent être conscients des différences entre les stratégies pour être en mesure de choisir la bonne.
- De nombreux langages de programmation modernes prennent en charge les types fonctionnels qui vous permettent d'implémenter différentes versions d'un algorithme dans un ensemble de fonctions anonymes. Ensuite, vous pouvez utiliser ces fonctions exactement comme vous avez utilisé les objets de stratégie, mais sans gonfler votre code avec des classes et des interfaces supplémentaires.