# Design pattern : Flyweight

Flyweight est un modèle de conception structurelle qui vous permet d'ajuster plus d'objets dans la quantité de RAM disponible en partageant des parties d'état communes entre plusieurs objets au lieu de conserver toutes les données de chaque objet.

### Ressources :

- https://refactoring.guru/design-patterns/flyweight

### Problématiques :

Pour vous amuser après de longues heures de travail, vous avez décidé de créer un jeu vidéo simple: les joueurs se déplaceraient sur une carte et se tireraient dessus. Vous avez choisi d'implémenter un système de particules réaliste et d'en faire une caractéristique distinctive du jeu. De grandes quantités de balles, de missiles et d'obus provenant d'explosions devraient voler partout sur la carte et offrir une expérience passionnante au joueur.

Une fois terminé, vous avez poussé le dernier commit, créé le jeu et l'avez envoyé à votre ami pour un essai routier. Même si le jeu fonctionnait parfaitement sur votre machine, votre ami n’a pas pu jouer pendant longtemps. Sur son ordinateur, le jeu n'arrêtait pas de planter après quelques minutes de jeu. Après avoir passé plusieurs heures à fouiller dans les journaux de débogage, vous avez découvert que le jeu plantait en raison d'une quantité insuffisante de RAM. Il s'est avéré que la plate-forme de votre ami était beaucoup moins puissante que votre propre ordinateur, et c'est pourquoi le problème est apparu si rapidement sur sa machine.

Le problème réel était lié à votre système de particules. Chaque particule, telle qu'une balle, un missile ou un éclat d'obus était représentée par un objet séparé contenant de nombreuses données. À un moment donné, lorsque le carnage sur l'écran d'un joueur a atteint son paroxysme, les particules nouvellement créées ne rentrent plus dans la RAM restante, le programme s'est donc planté.

### Solution :

Le modèle Flyweight vous suggère d'arrêter de stocker l'état extrinsèque à l'intérieur de l'objet. Au lieu de cela, vous devez passer cet état à des méthodes spécifiques qui en dépendent. Seul l'état intrinsèque reste dans l'objet, vous permettant de le réutiliser dans différents contextes. Par conséquent, vous auriez besoin de moins de ces objets, car ils ne diffèrent que par l’état intrinsèque, qui a beaucoup moins de variations que l’extrinsèque.

Revenons à notre jeu. En supposant que nous ayons extrait l'état extrinsèque de notre classe de particules, seuls trois objets différents suffiraient pour représenter toutes les particules du jeu: une balle, un missile et un éclat d'obus. Comme vous l’avez probablement deviné, un objet qui ne stocke que l’état intrinsèque est appelé poids mouche.

#### Extrinsic state storage

Dans notre cas, c'est l'objet principal Game qui stocke toutes les particules dans le champ de particules. Pour déplacer l'état extrinsèque dans cette classe, vous devez créer plusieurs champs de tableau pour stocker les coordonnées, les vecteurs et la vitesse de chaque particule individuelle. Mais ce n'est pas tout. Vous avez besoin d'un autre tableau pour stocker les références à un poids volumique spécifique qui représente une particule. Ces tableaux doivent être synchronisés pour que vous puissiez accéder à toutes les données d'une particule en utilisant le même index.

Une solution plus élégante consiste à créer une classe de contexte distincte qui stockerait l'état extrinsèque avec une référence à l'objet poids mouche. Cette approche nécessiterait de n'avoir qu'un seul tableau dans la classe conteneur.

Attends une seconde! N'aurons-nous pas besoin d'avoir autant de ces objets contextuels que nous en avions au tout début? Techniquement, oui. Mais le fait est que ces objets sont beaucoup plus petits qu'avant. Les champs les plus gourmands en mémoire ont été déplacés vers quelques objets de poids mouche. Désormais, un millier de petits objets contextuels peuvent réutiliser un seul objet poids lourd au lieu de stocker mille copies de ses données.

#### Flyweight and immutability

Étant donné que le même objet poids mouche peut être utilisé dans différents contextes, vous devez vous assurer que son état ne peut pas être modifié. Un poids volant ne doit initialiser son état qu'une seule fois, via les paramètres du constructeur. Il ne doit exposer aucun paramètre ni champ public à d’autres objets.

#### Flyweight factory

Pour un accès plus pratique à divers poids mouche, vous pouvez créer une méthode d'usine qui gère un pool d'objets de poids mouche existants. La méthode accepte l'état intrinsèque du poids mouche souhaité d'un client, recherche un objet poids mouche existant correspondant à cet état et le renvoie s'il a été trouvé. Sinon, il crée un nouveau poids mouche et l'ajoute à la piscine.

Il existe plusieurs options où cette méthode pourrait être placée. L'endroit le plus évident est un conteneur de poids mouche. Vous pouvez également créer une nouvelle classe d'usine. Ou vous pouvez rendre la méthode d'usine statique et la placer dans une classe de poids mouche réelle.


### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Flyweight uniquement lorsque votre programme doit prendre en charge un grand nombre d'objets qui rentrent à peine dans la RAM disponible.

### Comment l'implémenter ?

- Divisez les champs d'une classe qui deviendra un poids mouche en deux parties:
        l'état intrinsèque: les champs qui contiennent des données inchangées dupliquées sur de nombreux objets
        l'état extrinsèque: les champs qui contiennent des données contextuelles uniques à chaque objet

- Laissez les champs qui représentent l'état intrinsèque dans la classe, mais assurez-vous qu'ils sont immuables. Ils ne doivent prendre leurs valeurs initiales qu'à l'intérieur du constructeur.

- Passez en revue les méthodes qui utilisent des champs de l'état extrinsèque. Pour chaque champ utilisé dans la méthode, introduisez un nouveau paramètre et utilisez-le à la place du champ.

- Si vous le souhaitez, créez une classe d'usine pour gérer le pool de poids mouches. Il devrait vérifier un poids mouche existant avant d'en créer un nouveau. Une fois l'usine en place, les clients ne doivent demander que des poids mouches. Ils doivent décrire le poids mouche souhaité en transmettant son état intrinsèque à l'usine.

- Le client doit stocker ou calculer les valeurs de l'état extrinsèque (contexte) pour pouvoir appeler des méthodes d'objets flyweight. Pour des raisons de commodité, l'état extrinsèque ainsi que le champ de référencement de poids volants peuvent être déplacés vers une classe de contexte distincte.

### Avantages :

- Vous pouvez économiser beaucoup de RAM, en supposant que votre programme contienne des tonnes d'objets similaires.

### Inconvénients :

- Vous pouvez échanger de la RAM sur des cycles de processeur lorsque certaines des données de contexte doivent être recalculées chaque fois que quelqu'un appelle une méthode de poids mouche.
- Le code devient beaucoup plus compliqué. Les nouveaux membres de l'équipe se demanderont toujours pourquoi l'état d'une entité a été séparé de cette manière.