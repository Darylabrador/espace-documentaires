## Qu’est-ce qu’un design pattern ?

Un design pattern est une solution reproductible à un problème courant. C’est une description ou un modèle de résolution d’un problème qui peut être utilisé dans de nombreuses situations différentes. Il existe trois groupe de design pattern qui sont :

- Creational Patterns
- Structural Patterns
- Behavioral Patterns

## Le but d’un design pattern

Son but est d’optimiser le processus de développement en évitant les problèmes subtils qui peuvent causer des problèmes majeurs et améliorer la lisibilité du code pour les développeurs et les architectes qui sont familiers avec les patterns. Les design patterns fournissent des solutions générales, documentées dans un format qui ne nécessite pas de détails liés à un problème particulier. Ils peuvent s’appliquer à différents problèmes de manière global. 

<a href="https://refactoring.guru/design-patterns/examples"> Exemples de code </a>

## Creational Patterns

### Qu'est-ce que s'est ? 

Le "creational design patterns" fournis un ensemble de mécanisme pour la création d'objet qui va permettre d'augmenter la flexibilité et la réutilisation du code existant. On y retrouve donc les patterns ci dessous.


### Factory method

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/factory_method.md"> La "factory method" </a> est aussi connue sous le nom de "constructeur virtuel". Il s'agit ici d'un modèle de conception créative qui fournit une interface pour créer des objets dans une superclasse, mais permet aux sous-classes de modifier le type d'objets qui seront créés. Le code qui utilise la factory method (souvent appelée code client) ne voit pas de différence entre les produits réels renvoyés par les différentes sous-classes. Dans le cas d'un logiciel de logistique, le client traite tous les produits comme des transports abstraits. Le client sait que tous les objets de transport sont censés avoir la méthode de livraison, mais son fonctionnement n’est pas important pour le client.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/factory_method.md"> Voir le détail </a>


### Abstract Factory

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/abstract_factory.md">L' "Abstract Factory" </a> fournit une interface pour créer des familles d'objets liés ou dépendants sans spécifier leurs classes concrètes. Généralement, l'application crée un objet factory concret au stade de l'initialisation. Juste avant cela, l'application doit sélectionner le type factory en fonction de la configuration ou des paramètres d'environnement.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/abstract_factory.md"> Voir le détail </a>


### Builder

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/builder.md"> Le design pattern builder </a> est un modèle de conception créative qui permet de construire des objets complexes étape par étape. Ce modèle permet de produire différents types et représentations d'un objet en utilisant le même code de construction. Dans ce cas, il est suggèré d'extraire le code de construction d'objet de sa propre classe et de le déplacer vers des objets séparés appelés générateurs.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/builder.md"> Voir le détail </a>


### Prototype

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/prototype.md"> Le Design Pattern prototype </a> aussi connue sous le nom de "clone" est un modèle de conception créative qui permet de copier des objets existants sans rendre le code dépendant de leurs classes. Voici comment cela fonctionne: vous créez un ensemble d’objets, configurés de différentes manières. Lorsque vous avez besoin d’un objet comme celui que vous avez configuré, il vous suffit de cloner un prototype au lieu de créer un nouvel objet à partir de zéro.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/prototype.md"> Voir le détail </a>


### Singleton

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/singleton.md"> Le Design Pattern Singleton </a> est un modèle de conception créative qui permet de nous assurer qu'une classe n'a qu'une seule instance, tout en fournissant un point d'accès globale à cette instance.
 
<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/singleton.md"> Voir le détail </a>


## Structural patterns

Ces modèles de conception concernent tous la composition de classes et d'objets. Les modèles structurels de création de classes utilisent l'héritage pour composer des interfaces. Les modèles d'objet structurels définissent des moyens de composer des objets pour obtenir de nouvelles fonctionnalités. Plus précisément, ils expliquent comment assembler des objets et des classes dans des structures plus grandes tout en gardant ces structures flexibles et efficaces.

### Adapter

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/adapter.md"> Le patern design adapter </a> est aussi connu sous le nom de "Wrapper". Il s'agit ici d'un modle de conception structurelle qui permet aux objets avec des interfaces incompatobles de collaborer. Les adaptateurs peuvent non seulement convertir les données en différents formats, mais peuvent également aider les objets avec différentes interfaces à collaborer. Parfois, il est même possible de créer un adaptateur bidirectionnel capable de convertir les appels dans les deux sens.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/adapter.md"> Voir le détail </a>


### Bridge

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/bridge.md"> Le design pattern Bridge </a> est un modèle de conception structurelle qui vous permet de diviser une grande classe ou un ensemble de classes étroitement liées en deux hiérarchies distinctes (abstraction et implémentation) qui peuvent être développées indépendamment l'une de l'autre. Le modèle Bridge tente de résoudre ce problème en passant de l'héritage à la composition de l'objet. Cela signifie que vous extrayez l'une des dimensions dans une hiérarchie de classes distincte, de sorte que les classes d'origine référencent un objet de la nouvelle hiérarchie, au lieu d'avoir tous ses états et comportements dans une classe.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/bridge.md"> Voir le détail </a>


### Composite

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/composite.md"> Le design pattern Composite </a> est un modèle de conception structurelle qui vous permet de composer des objets en arborescence, puis de travailler avec ces structures comme s'il s'agissait d'objets individuels. Le modèle composite vous suggère de travailler avec des produits et des boîtes via une interface commune qui déclare une méthode de calcul du prix total.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/composite.md"> Voir le détail </a>


### Decorator

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/decorator.md"> Le design pattern Decorator</a> est un modèle de conception structurelle qui vous permet d'attacher de nouveaux comportements à des objets en plaçant ces objets dans des objets wrapper spéciaux contenant les comportements. «Wrapper» est le surnom alternatif du motif Decorator qui exprime clairement l'idée principale du motif. Un wrapper est un objet qui peut être lié à un objet cible. L'encapsuleur contient le même ensemble de méthodes que la cible et lui délègue toutes les demandes qu'il reçoit. Toutefois, le wrapper peut modifier le résultat en effectuant quelque chose avant ou après avoir transmis la demande à la cible.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/decorator.md"> Voir le détail </a>


### Facade

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/facade.md"> Le design pattern Façade </a> est un modèle de conception structurelle qui fournit une interface simplifiée à une bibliothèque, un cadre ou tout autre ensemble complexe de classes. C'est une classe qui fournit une interface simple à un sous-système complexe contenant de nombreuses pièces mobiles. Une façade peut fournir des fonctionnalités limitées par rapport au travail direct avec le sous-système. Cependant, il n'inclut que les fonctionnalités qui intéressent vraiment les clients.


<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/facade.md"> Voir le détail </a>


### Flyweight

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/flyweight.md"> Le design pattern Flyweight </a> est un modèle de conception structurelle qui vous permet d'ajuster plus d'objets dans la quantité de RAM disponible en partageant des parties d'état communes entre plusieurs objets au lieu de conserver toutes les données de chaque objet. Ce modèle suggère d'arrêter de stocker l'état extrinsèque à l'intérieur de l'objet. Au lieu de cela, vous devez passer cet état à des méthodes spécifiques qui en dépendent. Seul l'état intrinsèque reste dans l'objet, vous permettant de le réutiliser dans différents contextes. Par conséquent, vous auriez besoin de moins de ces objets, car ils ne diffèrent que par l’état intrinsèque, qui a beaucoup moins de variations que l’extrinsèque.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/flyweight.md"> Voir le détail </a>


### Proxy

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/proxy.md"> Le design pattern proxy </a> est un modèle de conception structurelle qui vous permet de fournir un substitut ou un espace réservé pour un autre objet. Un proxy contrôle l'accès à l'objet d'origine, vous permettant d'effectuer quelque chose avant ou après que la demande parvienne à l'objet d'origine. Il suggère de créer une nouvelle classe de proxy avec la même interface qu'un objet de service d'origine. Ensuite, vous mettez à jour votre application afin qu'elle transmette l'objet proxy à tous les clients de l'objet d'origine. À la réception d'une demande d'un client, le proxy crée un véritable objet de service et lui délègue tout le travail.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/proxy.md"> Voir le détail </a>


## Behavioral patterns

Ces modèles de conception concernent tous la communication des objets de Class. Les modèles comportementaux sont les modèles les plus spécifiquement concernés par la communication entre les objets. Autrement dit, ils concernent les algorithmes et l'attribution des responsabilités entre les objets.


### Chain responsability

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/chain_responsability.md">La chaîne de responsabilité</a> est un modèle de conception comportementale qui vous permet de transmettre des demandes le long d'une chaîne de gestionnaires. Lors de la réception d'une demande, chaque gestionnaire décide soit de traiter la demande, soit de la transmettre au gestionnaire suivant de la chaîne. Il est aussi connu sous le nom de CoR ou Chain of Command. Il suggère de lier des gestionnaires dans une chaîne. Chaque gestionnaire lié a un champ pour stocker une référence au gestionnaire suivant dans la chaîne. En plus de traiter une requête, les gestionnaires transmettent la requête plus loin dans la chaîne. La demande parcourt la chaîne jusqu'à ce que tous les gestionnaires aient eu la possibilité de la traiter.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/chain_responsability.md"> Voir le détail </a>


### Command

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/command.md"> Le design pattern commande</a> est un modèle de conception comportementale qui transforme une demande en un objet autonome contenant toutes les informations sur la demande. Cette transformation vous permet de paramétrer des méthodes avec différentes requêtes, de retarder ou de mettre en file d'attente l'exécution d'une requête et de prendre en charge les opérations annulables. Il est aussi connu sous le nom d'action ou transaction.

Dans le code, cela pourrait ressembler à ceci: un objet GUI appelle une méthode d'un objet de logique métier, en lui passant des arguments. Ce processus est généralement décrit comme un objet envoyant une autre requête.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/command.md"> Voir le détail </a>


### Iterator

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/iterator.md"> Le design pattern Iterator </a> est un modèle de conception comportementale qui vous permet de parcourir les éléments d'une collection sans exposer sa représentation sous-jacente (liste, pile, arbre, etc.). L'idée principale du modèle Iterator est d'extraire le comportement de traversée d'une collection dans un objet séparé appelé itérateur. Tous les itérateurs doivent implémenter la même interface. Cela rend le code client compatible avec n'importe quel type de collection ou n'importe quel algorithme de traversée tant qu'il existe un itérateur approprié. Si vous avez besoin d'un moyen spécial pour parcourir une collection, vous créez simplement une nouvelle classe d'itérateur, sans avoir à modifier la collection ou le client.


<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/iterator.md"> Voir le détail </a>


### Mediator

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/mediator.md"> Le design pattern  Mediator </a> est un modèle de conception comportementale qui vous permet de réduire les dépendances chaotiques entre les objets. Le modèle restreint les communications directes entre les objets et les oblige à collaborer uniquement via un objet médiateur. Il est aussi connu  sous le nom d'intermédiaire ou controller. Il suggère de cesser toute communication directe entre les composants que vous souhaitez rendre indépendants les uns des autres. Au lieu de cela, ces composants doivent collaborer indirectement, en appelant un objet médiateur spécial qui redirige les appels vers les composants appropriés. En conséquence, les composants ne dépendent que d'une seule classe de médiateur au lieu d'être couplés à des dizaines de leurs collègues.


<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/mediator.md"> Voir le détail </a>


### Memento

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/memento.md"> Le design pattern Memento </a> est un modèle de conception comportementale qui vous permet d'enregistrer et de restaurer l'état précédent d'un objet sans révéler les détails de son implémentation. Il est aussi connue sous le nom de Snapshot. Il délègue la création des instantanés d'état au propriétaire réel de cet état, l'objet créateur. Par conséquent, au lieu d’autres objets essayant de copier l’état de l’éditeur depuis «l’extérieur», la classe d’éditeur elle-même peut créer l’instantané car elle a un accès complet à son propre état.

Il suggère de stocker la copie de l'état de l'objet dans un objet spécial appelé memento. Le contenu du souvenir n'est accessible à aucun autre objet, à l'exception de celui qui l'a produit. Les autres objets doivent communiquer avec les mémentos en utilisant une interface limitée qui peut permettre d’extraire les métadonnées de l’instantané (heure de création, le nom de l’opération effectuée, etc.), mais pas l’état de l’objet original contenu dans l’instantané.


<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/memento.md"> Voir le détail </a>


### Observer

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/observer.md"> Le design pattern Observer </a> est un modèle de conception comportementale qui vous permet de définir un mécanisme d'abonnement pour informer plusieurs objets de tout événement survenant à l'objet qu'ils observent. Il est aussi connu sous le nom de Event-Subscriber ou Listener. 

Il suggère que vous ajoutiez un mécanisme d'abonnement à la classe d'éditeur afin que les objets individuels puissent s'abonner ou se désabonner d'un flux d'événements provenant de cet éditeur. N'aie pas peur! Tout n’est pas aussi compliqué qu’il y paraît. 

En réalité, ce mécanisme consiste en :
    1) un champ de tableau pour stocker une liste de références aux objets abonnés
    2) plusieurs méthodes publiques qui permettent d'ajouter des abonnés et de les supprimer de cette liste.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/observer.md"> Voir le détail </a>


### State

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/state.md"> Le design pattern "état" </a>  est un modèle de conception comportementale qui permet à un objet de modifier son comportement lorsque son état interne change. Il semble que l'objet ait changé de classe. Il suggère de créer de nouvelles classes pour tous les états possibles d'un objet et d'extraire tous les comportements spécifiques à l'état dans ces classes. Au lieu d'implémenter seul tous les comportements, l'objet d'origine, appelé contexte, stocke une référence à l'un des objets d'état qui représente son état actuel et délègue tout le travail lié à l'état à cet objet.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/state.md"> Voir le détail </a>


### Strategy

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/strategy.md"> Le design pattern "Strategy" </a> est un modèle de conception comportementale qui vous permet de définir une famille d'algorithmes, de placer chacun d'eux dans une classe distincte et de rendre leurs objets interchangeables. Il suggère que vous preniez une classe qui fait quelque chose de spécifique de nombreuses manières différentes et que vous extrayiez tous ces algorithmes dans des classes distinctes appelées stratégies. La classe d'origine, appelée context, doit avoir un champ pour stocker une référence à l'une des stratégies. Le contexte délègue le travail à un objet de stratégie lié au lieu de l'exécuter seul.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/strategy.md"> Voir le détail </a>


### Template method

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/template_method.md"> Le design pattern "template method" </a> est un modèle de conception comportementale qui définit le squelette d'un algorithme dans la superclasse, mais permet aux sous-classes de remplacer des étapes spécifiques de l'algorithme sans changer sa structure. Il suggère de décomposer un algorithme en une série d'étapes, de transformer ces étapes en méthodes et de placer une série d'appels à ces méthodes dans une méthode de modèle unique. Les étapes peuvent être abstraites ou avoir une implémentation par défaut. Pour utiliser l'algorithme, le client est censé fournir sa propre sous-classe, implémenter toutes les étapes abstraites et remplacer certaines des étapes facultatives si nécessaire (mais pas la méthode du modèle elle-même).

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/template_method.md"> Voir le détail </a>


### Visitor

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/visitor.md"> Le design pattern "visitor" </a> est un modèle de conception comportementale qui vous permet de séparer les algorithmes des objets sur lesquels ils opèrent. Il suggère de placer le nouveau comportement dans une classe distincte appelée visiteur, au lieu d'essayer de l'intégrer dans des classes existantes. L’objet d’origine qui devait exécuter le comportement est maintenant transmis à l’une des méthodes du visiteur en tant qu’argument, permettant à la méthode d’accéder à toutes les données nécessaires contenues dans l’objet.

<a href="https://github.com/Darylabrador/espace-documentaires/blob/design-pattern/visitor.md"> Voir le détail </a>