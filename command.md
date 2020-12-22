# Design pattern : Command

La commande est un modèle de conception comportementale qui transforme une demande en un objet autonome contenant toutes les informations sur la demande. Cette transformation vous permet de paramétrer des méthodes avec différentes requêtes, de retarder ou de mettre en file d'attente l'exécution d'une requête et de prendre en charge les opérations annulables. Il est aussi connu sous le nom d'action ou transaction.

### Ressources :

- https://refactoring.guru/design-patterns/command

### Problématiques :

Imaginez que vous travaillez sur une nouvelle application d'édition de texte. Votre tâche actuelle est de créer une barre d'outils avec un tas de boutons pour diverses opérations de l'éditeur. Vous avez créé une classe Button très soignée qui peut être utilisée pour les boutons de la barre d'outils, ainsi que pour les boutons génériques dans diverses boîtes de dialogue.

Bien que tous ces boutons se ressemblent, ils sont tous censés faire des choses différentes. Où mettriez-vous le code des différents gestionnaires de clics de ces boutons? La solution la plus simple consiste à créer des tonnes de sous-classes pour chaque endroit où le bouton est utilisé. Ces sous-classes contiendraient le code qui devrait être exécuté sur un clic de bouton.

Avant longtemps, vous vous rendez compte que cette approche est profondément imparfaite. Premièrement, vous avez un nombre énorme de sous-classes, et ce serait bien si vous ne risquiez pas de casser le code de ces sous-classes à chaque fois que vous modifiez la classe Button de base. En termes simples, votre code GUI est devenu maladroitement dépendant du code volatil de la logique métier.

Et voici la partie la plus moche. Certaines opérations, telles que copier / coller du texte, devraient être appelées à partir de plusieurs endroits. Par exemple, un utilisateur peut cliquer sur un petit bouton «Copier» dans la barre d'outils, ou copier quelque chose via le menu contextuel, ou simplement appuyer sur Ctrl + C sur le clavier.

Au départ, lorsque notre application n'avait que la barre d'outils, il était normal de placer l'implémentation de diverses opérations dans les sous-classes de boutons. En d'autres termes, avoir le code pour copier du texte dans la sous-classe CopyButton était très bien. Mais ensuite, lorsque vous implémentez des menus contextuels, des raccourcis et d’autres éléments, vous devez soit dupliquer le code de l’opération dans de nombreuses classes, soit rendre les menus dépendants des boutons, ce qui est une option encore pire.


### Solution :

Une bonne conception logicielle est souvent basée sur le principe de la séparation des préoccupations, ce qui aboutit généralement à diviser une application en couches. L'exemple le plus courant: une couche pour l'interface utilisateur graphique et une autre couche pour la logique métier. La couche GUI est chargée de restituer une belle image à l'écran, de capturer toute entrée et d'afficher les résultats de ce que font l'utilisateur et l'application. Cependant, lorsqu'il s'agit de faire quelque chose d'important, comme calculer la trajectoire de la lune ou rédiger un rapport annuel, la couche GUI délègue le travail à la couche sous-jacente de la logique métier.

Dans le code, cela pourrait ressembler à ceci: un objet GUI appelle une méthode d'un objet de logique métier, en lui passant des arguments. Ce processus est généralement décrit comme un objet envoyant une autre requête.

Lorsque nous appliquons le modèle de commande, nous n'avons plus besoin de toutes ces sous-classes de boutons pour implémenter divers comportements de clic. Il suffit de placer un seul champ dans la classe Button de base qui stocke une référence à un objet de commande et de faire exécuter cette commande par le bouton en un clic. Vous allez implémenter un tas de classes de commandes pour chaque opération possible et les lier avec des boutons particuliers, en fonction du comportement prévu des boutons.

D'autres éléments de l'interface graphique, tels que des menus, des raccourcis ou des boîtes de dialogue entières, peuvent être implémentés de la même manière. Ils seront liés à une commande qui est exécutée lorsqu'un utilisateur interagit avec l'élément GUI. Comme vous l’avez probablement deviné, les éléments liés aux mêmes opérations seront liés aux mêmes commandes, évitant ainsi toute duplication de code. En conséquence, les commandes deviennent une couche intermédiaire pratique qui réduit le couplage entre l'interface graphique et les couches de logique métier. Et ce n'est qu'une fraction des avantages que le modèle Command peut offrir!

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle de commande lorsque vous souhaitez paramétrer des objets avec des opérations.
- Utilisez le modèle de commande lorsque vous souhaitez mettre des opérations en file d'attente, planifier leur exécution ou les exécuter à distance.
- Utilisez le modèle de commande lorsque vous souhaitez implémenter des opérations réversibles.

### Comment l'implémenter ?

- Déclarez l'interface de commande avec une seule méthode d'exécution.

- Commencez à extraire les requêtes dans des classes de commandes concrètes qui implémentent l'interface de commande. Chaque classe doit avoir un ensemble de champs pour stocker les arguments de la demande avec une référence à l'objet récepteur réel. Toutes ces valeurs doivent être initialisées via le constructeur de la commande.

- Identifiez les classes qui agiront en tant qu'expéditeurs. Ajoutez les champs pour stocker les commandes dans ces classes. Les expéditeurs doivent communiquer avec leurs commandes uniquement via l'interface de commande. Les expéditeurs ne créent généralement pas d’objets de commande eux-mêmes, mais les récupèrent à partir du code client.

- Changez les expéditeurs pour qu'ils exécutent la commande au lieu d'envoyer une demande directement au destinataire.

- Le client doit initialiser les objets dans l'ordre suivant:
    - Créez des récepteurs.
    - Créez des commandes et associez-les aux récepteurs si nécessaire.
    - Créez des expéditeurs et associez-les à des commandes spécifiques.

### Avantages :

- Principe de responsabilité unique. Vous pouvez découpler les classes qui appellent des opérations des classes qui effectuent ces opérations.
- Principe ouvert / fermé. Vous pouvez introduire de nouvelles commandes dans l'application sans casser le code client existant.
- Vous pouvez implémenter annuler / rétablir.
- Vous pouvez implémenter une exécution différée des opérations.
- Vous pouvez assembler un ensemble de commandes simples en une commande complexe.

### Inconvénients :

- Le code peut devenir plus compliqué car vous introduisez une toute nouvelle couche entre les expéditeurs et les destinataires.