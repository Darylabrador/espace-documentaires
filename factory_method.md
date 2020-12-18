# Design pattern : Factory method

La "factory method" est aussi connue sous le nom de "constructeur virtuel". Il s'agit ici d'un modèle de conception créative qui fournit une interface
pour créer des objets dans une superclasse, mais permet aux sous-classes de modifier le type d'objets qui seront créés.

### Ressources pour aller plus loin :

- https://refactoring.guru/design-patterns/factory-method

### Problématique :

Imaginons que nous developpons une première version d'une application de logistique qui peut gérer uniquement le transport de camions et que la majorité du code se trouve dans la class Truck. Après un certain temps, l'application devient très populaire. Chaque jour, il a des demande d'entreprises de transport maritime pour intégrer la logistique maritine dans l'application. L'ajout de la classe Ships dans l'application
nécessiterait d'apporter des modifications à l'ensemble de la base de code. Et cela risque de ce reproduire à chaque fois qu'on ajoute un autre type de transport. En conséquence, on va se retrouver avec diverse conditions qui modifient le comportement de l'application en fonction de la classe d'objets de transport.

### Solution :

La "factory method", nous suggère de remplacer l'appel de l'opérateur "new" de l'objet de construction par l'utilisation d'un appel spécial. On utilise toujours l'opérateur "new" mais depuis la "factory method". Les objets retourner par la factory method sont souvent appelés des "produits". En déplaçant l'appel du constructeur d'une partie du programme à un autre (sous classe), on peut changer la classe des produits créer par la méthode.

Une limitation se situe au niveau des sous-classes qui peuvent renvoyer différents types de produits uniquement si ces produits ont une classe de base ou une interface commune. En outre, la factory method dans la classe de base doit avoir son type de retour déclarer comme interface. 

Par exemple, les classes Trucks et Ship doivent implémenter l'interface transport qui déclare une méthode appelé livrer. Chaque classe met en œuvre cette méthode différemment: les camions livrent les marchandises par voie terrestre, les navires livrent les marchandises par mer. La méthode factory de la classe RoadLogistics renvoie des objets camion, tandis que la méthode factory de la classe SeaLogistics renvoie des navires.

Le code qui utilise la factory method (souvent appelée code client) ne voit pas de différence entre les produits réels renvoyés par les différentes sous-classes. Le client traite tous les produits comme des transports abstraits. Le client sait que tous les objets de transport sont censés avoir la méthode de livraison, mais son fonctionnement n’est pas important pour le client.


### Quand est ce qu'il faut l'appliquer ?

- Utilisez la méthode Factory lorsque vous ne savez pas à l'avance les types et dépendances exacts des objets avec lesquels votre code doit fonctionner.
- Utilisez la méthode Factory lorsque vous souhaitez fournir aux utilisateurs de votre bibliothèque ou infrastructure un moyen d'étendre ses composants internes.
- Utilisez la méthode Factory lorsque vous souhaitez enregistrer des ressources système en réutilisant des objets existants au lieu de les reconstruire à chaque fois.

### Comment l'implémenter ?

- Faites en sorte que tous les produits suivent la même interface. Cette interface doit déclarer des méthodes qui ont du sens dans chaque produit.

- Ajoutez une méthode de fabrique vide dans la classe de créateur. Le type de retour de la méthode doit correspondre à l'interface de produit commune.

- Dans le code du créateur, recherchez toutes les références aux constructeurs de produits. Un par un, remplacez-les par des appels à la méthode de fabrique, tout en extrayant le code de création de produit dans la méthode de fabrique.

- Vous devrez peut-être ajouter un paramètre temporaire à la méthode de fabrique pour contrôler le type de produit retourné.

- À ce stade, le code de la méthode d'usine peut sembler assez moche. Il peut avoir un grand opérateur de commutation qui sélectionne la classe de produit à instancier. Mais ne vous inquiétez pas, nous allons résoudre le problème assez tôt.

- Maintenant, créez un ensemble de sous-classes de créateur pour chaque type de produit répertorié dans la méthode d'usine. Remplacez la méthode d'usine dans les sous-classes et extrayez les bits appropriés du code de construction de la méthode de base. S'il y a trop de types de produits et qu'il n'est pas judicieux de créer des sous-classes pour tous, vous pouvez réutiliser le paramètre de contrôle de la classe de base dans les sous-classes. Par exemple, imaginez que vous ayez la hiérarchie de classes suivante: la classe Mail de base avec quelques sous-classes: AirMail et GroundMail; les classes de transport sont Avion, Camion et Train. Alors que la classe AirMail n'utilise que des objets Plan, GroundMail peut fonctionner avec des objets Camion et Train. Vous pouvez créer une nouvelle sous-classe (par exemple TrainMail) pour gérer les deux cas, mais il existe une autre option. Le code client peut passer un argument à la méthode de fabrique de la classe GroundMail pour contrôler le produit qu'il souhaite recevoir. Si, après toutes les extractions, la méthode de fabrique de base est devenue vide, vous pouvez la rendre abstraite. S'il reste quelque chose, vous pouvez en faire un comportement par défaut de la méthode.

### Avantages :

Vous évitez un couplage étroit entre le créateur et les produits concrèts.

Principe de responsabilité unique. Vous pouvez déplacer le code de création de produit en un seul endroit dans le programme, ce qui facilite la prise en charge du code.

Principe ouvert / fermé. Vous pouvez introduire de nouveaux types de produits dans le programme sans casser le code client existant.

### Inconvénients :

Le code peut devenir plus compliqué car vous devez introduire de nombreuses nouvelles sous-classes pour implémenter le modèle. Le meilleur des cas est lorsque vous introduisez le modèle dans une hiérarchie existante de classes de créateur.