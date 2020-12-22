# Design pattern : Chain responsability

La chaîne de responsabilité est un modèle de conception comportementale qui vous permet de transmettre des demandes le long d'une chaîne de gestionnaires. Lors de la réception d'une demande, chaque gestionnaire décide soit de traiter la demande, soit de la transmettre au gestionnaire suivant de la chaîne. Il est aussi connu sous le nom de CoR ou Chain of Command.

### Ressources :

- https://refactoring.guru/design-patterns/chain-of-responsibility

### Problématiques :

Imaginez que vous travaillez sur un système de commande en ligne. Vous souhaitez restreindre l'accès au système afin que seuls les utilisateurs authentifiés puissent créer des commandes. En outre, les utilisateurs disposant d'autorisations administratives doivent avoir un accès complet à toutes les commandes.

Après un peu de planification, vous vous êtes rendu compte que ces contrôles doivent être effectués de manière séquentielle. L’application peut tenter d’authentifier un utilisateur auprès du système chaque fois qu’elle reçoit une demande contenant les informations d’identification de l’utilisateur. Cependant, si ces informations d'identification ne sont pas correctes et que l'authentification échoue, il n'y a aucune raison de procéder à d'autres vérifications.

Au cours des prochains mois, vous avez mis en œuvre plusieurs autres de ces contrôles séquentiels. Un de vos collègues a suggéré qu’il n’était pas sûr de transmettre des données brutes directement au système de commande. Vous avez donc ajouté une étape de validation supplémentaire pour nettoyer les données d'une demande. Plus tard, quelqu'un a remarqué que le système était vulnérable au craquage de mots de passe par force brute. Pour annuler cela, vous avez rapidement ajouté une vérification qui filtre les demandes répétées ayant échoué provenant de la même adresse IP. Quelqu'un d'autre a suggéré que vous pourriez accélérer le système en renvoyant les résultats mis en cache sur des demandes répétées contenant les mêmes données. Par conséquent, vous avez ajouté une autre vérification qui permet à la demande de passer au système uniquement s'il n'y a pas de réponse mise en cache appropriée.

Le code de vérification, qui avait déjà ressemblé à un gâchis, est devenu de plus en plus gonflé à mesure que vous ajoutiez chaque nouvelle fonctionnalité. Changer un chèque affectait parfois les autres. Pire encore, lorsque vous avez essayé de réutiliser les vérifications pour protéger d'autres composants du système, vous avez dû dupliquer une partie du code car ces composants nécessitaient certaines vérifications, mais pas toutes. Le système est devenu très difficile à comprendre et coûteux à entretenir. Vous avez lutté avec le code pendant un certain temps, jusqu'au jour où vous avez décidé de tout refactoriser.

### Solution :

Comme beaucoup d'autres modèles de conception comportementale, la chaîne de responsabilité repose sur la transformation de comportements particuliers en objets autonomes appelés gestionnaires. Dans notre cas, chaque vérification doit être extraite dans sa propre classe avec une seule méthode qui effectue la vérification. La requête, avec ses données, est transmise à cette méthode en tant qu'argument.

Le modèle suggère que vous liez ces gestionnaires dans une chaîne. Chaque gestionnaire lié a un champ pour stocker une référence au gestionnaire suivant dans la chaîne. En plus de traiter une requête, les gestionnaires transmettent la requête plus loin dans la chaîne. La demande parcourt la chaîne jusqu'à ce que tous les gestionnaires aient eu la possibilité de la traiter.

Voici la meilleure partie: un gestionnaire peut décider de ne pas transmettre la demande plus bas dans la chaîne et d'arrêter efficacement tout traitement ultérieur.

Dans notre exemple avec les systèmes de commande, un gestionnaire effectue le traitement et décide ensuite s'il doit transmettre la demande plus bas dans la chaîne. En supposant que la demande contient les bonnes données, tous les gestionnaires peuvent exécuter leur comportement principal, qu'il s'agisse de vérifications d'authentification ou de mise en cache.

Cependant, il existe une approche légèrement différente (et c'est un peu plus canonique) dans laquelle, lors de la réception d'une requête, un gestionnaire décide s'il peut la traiter. S'il le peut, il ne transmet plus la demande. C'est donc soit un seul gestionnaire qui traite la demande, soit aucun gestionnaire. Cette approche est très courante lorsqu'il s'agit d'événements dans des piles d'éléments dans une interface utilisateur graphique.

Par exemple, lorsqu'un utilisateur clique sur un bouton, l'événement se propage à travers la chaîne d'éléments d'interface graphique qui commence par le bouton, suit ses conteneurs (comme des formulaires ou des panneaux) et se termine par la fenêtre principale de l'application. L'événement est traité par le premier élément de la chaîne capable de le gérer. Cet exemple est également remarquable car il montre qu'une chaîne peut toujours être extraite d'une arborescence d'objets.

Il est essentiel que toutes les classes de gestionnaires implémentent la même interface. Chaque gestionnaire concret ne doit se soucier que du suivant ayant la méthode execute. De cette façon, vous pouvez composer des chaînes au moment de l'exécution, en utilisant divers gestionnaires sans coupler votre code à leurs classes concrètes.


### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Chaîne de responsabilité lorsque votre programme est censé traiter différents types de demandes de différentes manières, mais que les types exacts de demandes et leurs séquences sont inconnus à l'avance.
- Utilisez le modèle lorsqu'il est essentiel d'exécuter plusieurs gestionnaires dans un ordre particulier.
- Utilisez le modèle CoR lorsque l'ensemble des gestionnaires et leur ordre sont censés changer au moment de l'exécution.

### Comment l'implémenter ?

- Déclarez l'interface du gestionnaire et décrivez la signature d'une méthode de gestion des requêtes.

- Décidez de la manière dont le client transmettra les données de la demande à la méthode. Le moyen le plus flexible est de convertir la requête en objet et de la transmettre à la méthode de gestion en tant qu'argument.

- Pour éliminer le code réutilisable en double dans les gestionnaires concrets, il peut être utile de créer une classe de gestionnaire de base abstraite, dérivée de l'interface du gestionnaire.

- Cette classe doit avoir un champ pour stocker une référence au prochain gestionnaire de la chaîne. Pensez à rendre la classe immuable. Cependant, si vous prévoyez de modifier les chaînes lors de l'exécution, vous devez définir un setter pour modifier la valeur du champ de référence.

- Vous pouvez également implémenter le comportement par défaut pratique pour la méthode de gestion, qui consiste à transmettre la demande à l’objet suivant à moins qu’il n’en reste aucun. Les gestionnaires concrets pourront utiliser ce comportement en appelant la méthode parente.

- Une par une, créez des sous-classes de gestionnaires concrets et implémentez leurs méthodes de gestion. Chaque gestionnaire doit prendre deux décisions lors de la réception d'une demande:
    - S'il traitera la demande.
    - S'il transmettra la demande le long de la chaîne.

- Le client peut soit assembler des chaînes seul, soit recevoir des chaînes prédéfinies à partir d'autres objets. Dans ce dernier cas, vous devez implémenter certaines classes d'usine pour construire des chaînes en fonction des paramètres de configuration ou d'environnement.

- Le client peut déclencher n'importe quel gestionnaire de la chaîne, pas seulement le premier. La demande sera transmise le long de la chaîne jusqu'à ce qu'un gestionnaire refuse de la passer plus loin ou jusqu'à ce qu'elle atteigne la fin de la chaîne.

- En raison de la nature dynamique de la chaîne, le client doit être prêt à gérer les scénarios suivants:
    - La chaîne peut être constituée d'un seul maillon.
    - Certaines demandes peuvent ne pas atteindre la fin de la chaîne.
    - D'autres peuvent atteindre la fin de la chaîne sans être manipulés.


### Avantages :

- Vous pouvez contrôler l'ordre de traitement des demandes.
- Principe de responsabilité unique. Vous pouvez découpler les classes qui appellent des opérations des classes qui effectuent des opérations.
- Principe ouvert / fermé. Vous pouvez introduire de nouveaux gestionnaires dans l'application sans casser le code client existant.

### Inconvénients :

- Certaines demandes peuvent ne pas être traitées.