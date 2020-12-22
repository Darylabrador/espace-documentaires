# Design pattern : State

L'état est un modèle de conception comportementale qui permet à un objet de modifier son comportement lorsque son état interne change. Il semble que l'objet ait changé de classe.

### Ressources :

- https://refactoring.guru/design-patterns/state

### Problématiques :

Le modèle d'état est étroitement lié au concept de machine à états finis. L’idée principale est qu’à tout moment, il existe un nombre fini d’états dans lesquels un programme peut se trouver. Dans un état unique, le programme se comporte différemment et le programme peut être basculé d’un état à un autre instantanément. Cependant, en fonction d'un état actuel, le programme peut ou non basculer vers certains autres états. Ces règles de commutation, appelées transitions, sont également finies et prédéterminées.

Les machines à états sont généralement implémentées avec de nombreux opérateurs conditionnels (if ou switch) qui sélectionnent le comportement approprié en fonction de l'état actuel de l'objet. En général, cet «état» n’est qu’un ensemble de valeurs des champs de l’objet. Même si vous n’avez jamais entendu parler de machines à états finis auparavant, vous avez probablement implémenté un état au moins une fois. La structure de code suivante vous dit-elle quelque chose?

La plus grande faiblesse d'une machine à états basée sur des conditions se révèle une fois que nous commençons à ajouter de plus en plus d'états et de comportements dépendants de l'état à la classe Document. La plupart des méthodes contiennent des conditions monstrueuses qui choisissent le comportement approprié d'une méthode en fonction de l'état actuel. Un code comme celui-ci est très difficile à maintenir car toute modification de la logique de transition peut nécessiter de changer les conditions d'état dans chaque méthode.

Le problème a tendance à s'aggraver à mesure qu'un projet évolue. Il est assez difficile de prévoir tous les états et transitions possibles au stade de la conception. Par conséquent, une machine à états allégée construite avec un ensemble limité de conditions peut se transformer en un désordre gonflé au fil du temps.

### Solution :

Le modèle State vous suggère de créer de nouvelles classes pour tous les états possibles d'un objet et d'extraire tous les comportements spécifiques à l'état dans ces classes. Au lieu d'implémenter seul tous les comportements, l'objet d'origine, appelé contexte, stocke une référence à l'un des objets d'état qui représente son état actuel et délègue tout le travail lié à l'état à cet objet.

Pour faire passer le contexte dans un autre état, remplacez l'objet d'état actif par un autre objet qui représente ce nouvel état. Cela n'est possible que si toutes les classes d'état suivent la même interface et que le contexte lui-même fonctionne avec ces objets via cette interface. Cette structure peut ressembler au modèle de stratégie, mais il existe une différence essentielle. Dans le modèle d'état, les états particuliers peuvent être conscients l'un de l'autre et initier des transitions d'un état à un autre, alors que les stratégies ne se connaissent presque jamais.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle State lorsque vous avez un objet qui se comporte différemment en fonction de son état actuel, que le nombre d'états est énorme et que le code spécifique à l'état change fréquemment.
- Utilisez le modèle lorsque vous avez une classe polluée par des conditions conditionnelles massives qui modifient le comportement de la classe en fonction des valeurs actuelles des champs de la classe.
- Utilisez State lorsque vous avez beaucoup de code dupliqué dans des états et des transitions similaires d'une machine à états basée sur des conditions.


### Comment l'implémenter ?

- Décidez de la classe qui servira de contexte. Il peut s'agir d'une classe existante qui a déjà le code dépendant de l'état; ou une nouvelle classe, si le code spécifique à l'état est distribué sur plusieurs classes.

- Déclarez l'interface d'état. Bien qu'elle puisse refléter toutes les méthodes déclarées dans le contexte, visez uniquement celles qui peuvent contenir un comportement spécifique à un état.

- Pour chaque état réel, créez une classe qui dérive de l'interface d'état. Passez ensuite en revue les méthodes du contexte et extrayez tout le code lié à cet état dans votre classe nouvellement créée.

- Lors du déplacement du code vers la classe state, vous pourriez découvrir qu'il dépend de membres privés du contexte. Il existe plusieurs solutions de contournement:
    Rendez ces champs ou méthodes publics.
    Transformez le comportement que vous extrayez en une méthode publique dans le contexte et appelez-le à partir de la classe d'état. Cette méthode est moche mais rapide et vous pouvez toujours la réparer plus tard.
    Imbriquez les classes d'état dans la classe de contexte, mais uniquement si votre langage de programmation prend en charge les classes d'imbrication.

- Dans la classe context, ajoutez un champ de référence du type d'interface d'état et un setter public qui permet de remplacer la valeur de ce champ.

- Passez à nouveau en revue la méthode du contexte et remplacez les conditions d'état vides par des appels aux méthodes correspondantes de l'objet d'état.

- Pour changer l'état du contexte, créez une instance de l'une des classes d'état et transmettez-la au contexte. Vous pouvez le faire dans le contexte lui-même, ou dans divers états, ou dans le client. Partout où cela est fait, la classe devient dépendante de la classe d'état concrète qu'elle instancie.

### Avantages :

- Principe de responsabilité unique. Organisez le code lié à des états particuliers en classes distinctes.
- Principe ouvert / fermé. Introduisez de nouveaux états sans changer les classes d'états existantes ou le contexte.
- Simplifiez le code du contexte en éliminant les conditions conditionnelles de machine à états volumineuses.

### Inconvénients :

- L'application du modèle peut être excessive si une machine d'état n'a que quelques états ou change rarement.