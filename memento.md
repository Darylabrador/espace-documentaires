# Design pattern : Memento

Memento est un modèle de conception comportementale qui vous permet d'enregistrer et de restaurer l'état précédent d'un objet sans révéler les détails de son implémentation. Il est aussi connue sous le nom de Snapshot.

### Ressources :

- https://refactoring.guru/design-patterns/memento

### Problématiques :

Imaginez que vous créez une application d'édition de texte. En plus de l'édition de texte simple, votre éditeur peut formater du texte, insérer des images en ligne, etc.

À un moment donné, vous avez décidé de laisser les utilisateurs annuler toutes les opérations effectuées sur le texte. Cette fonctionnalité est devenue si courante au fil des ans que de nos jours, les gens s'attendent à ce que chaque application l'ait. Pour la mise en œuvre, vous avez choisi une approche directe. Avant d'effectuer toute opération, l'application enregistre l'état de tous les objets et l'enregistre dans un espace de stockage. Plus tard, lorsqu'un utilisateur décide d'annuler une action, l'application récupère le dernier instantané de l'historique et l'utilise pour restaurer l'état de tous les objets.

Pensons à ces instantanés d’état. Comment en produiriez-vous exactement un? Vous devrez probablement parcourir tous les champs d'un objet et copier leurs valeurs dans le stockage. Cependant, cela ne fonctionnerait que si l'objet avait des restrictions d'accès assez assouplies à son contenu. Malheureusement, la plupart des objets réels ne laisseront pas les autres y jeter un œil aussi facilement, cachant toutes les données importantes dans des champs privés.

Ignorez ce problème pour le moment et supposons que nos objets se comportent comme des hippies: préférer les relations ouvertes et garder leur état public. Bien que cette approche résoudrait le problème immédiat et vous permettrait de produire des instantanés des états des objets à volonté, elle pose encore de sérieux problèmes. À l'avenir, vous pourriez décider de refactoriser certaines des classes d'éditeur, ou d'ajouter ou de supprimer certains des champs. Cela semble facile, mais cela nécessiterait également de changer les classes chargées de copier l'état des objets affectés.

Mais il y a plus. Examinons les "instantanés" réels de l'état de l'éditeur. Quelles données contient-il? Au minimum, il doit contenir le texte réel, les coordonnées du curseur, la position de défilement actuelle, etc. Pour créer un instantané, vous devez collecter ces valeurs et les placer dans une sorte de conteneur.

Très probablement, vous allez stocker beaucoup de ces objets conteneurs dans une liste qui représenterait l'historique. Par conséquent, les conteneurs finiraient probablement par être des objets d'une classe. La classe n’aurait presque pas de méthodes, mais de nombreux champs reflétant l’état de l’éditeur. Pour permettre à d'autres objets d'écrire et de lire des données depuis et vers un instantané, vous devrez probablement rendre ses champs publics. Cela exposerait tous les états de l'éditeur, privés ou non. Les autres classes deviendraient dépendantes de chaque petit changement de la classe snapshot, qui se produirait autrement dans les champs et méthodes privés sans affecter les classes externes.

Il semble que nous ayons atteint une impasse: soit vous exposez tous les détails internes des classes, ce qui les rend trop fragiles, soit vous restreignez l'accès à leur état, ce qui rend impossible la production d'instantanés. Existe-t-il un autre moyen d'implémenter le "undo"?


### Solution :

Tous les problèmes que nous venons de rencontrer sont causés par une encapsulation interrompue. Certains objets essaient de faire plus qu'ils ne le devraient. Pour collecter les données nécessaires à l'exécution d'une action, ils envahissent l'espace privé d'autres objets au lieu de laisser ces objets effectuer l'action réelle.

Le modèle Memento délègue la création des instantanés d'état au propriétaire réel de cet état, l'objet créateur. Par conséquent, au lieu d’autres objets essayant de copier l’état de l’éditeur depuis «l’extérieur», la classe d’éditeur elle-même peut créer l’instantané car elle a un accès complet à son propre état.

Le modèle suggère de stocker la copie de l'état de l'objet dans un objet spécial appelé memento. Le contenu du souvenir n'est accessible à aucun autre objet, à l'exception de celui qui l'a produit. Les autres objets doivent communiquer avec les mémentos en utilisant une interface limitée qui peut permettre d’extraire les métadonnées de l’instantané (heure de création, le nom de l’opération effectuée, etc.), mais pas l’état de l’objet original contenu dans l’instantané.

Une telle politique restrictive vous permet de stocker des souvenirs dans d'autres objets, généralement appelés gardiens. Étant donné que le gardien ne travaille avec le souvenir que via l’interface limitée, il n’est pas en mesure de modifier l’état stocké à l’intérieur du souvenir. Dans le même temps, l'auteur a accès à tous les champs à l'intérieur du memento, lui permettant de restaurer son état précédent à volonté.

Dans notre exemple d'éditeur de texte, nous pouvons créer une classe d'historique distincte pour agir en tant que gardien. Une pile de souvenirs stockés à l'intérieur du gardien augmentera chaque fois que l'éditeur est sur le point d'exécuter une opération. Vous pouvez même afficher cette pile dans l'interface utilisateur de l'application, en affichant l'historique des opérations précédemment effectuées à un utilisateur.

Lorsqu'un utilisateur déclenche l'annulation, l'historique récupère le souvenir le plus récent de la pile et le renvoie à l'éditeur, en demandant une restauration. Puisque l'éditeur a un accès complet au memento, il change son propre état avec les valeurs extraites du memento.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Memento lorsque vous souhaitez produire des instantanés de l’état de l’objet afin de pouvoir restaurer un état antérieur de l’objet.
- Utilisez le modèle lorsque l’accès direct aux champs / getters / setters de l’objet viole son encapsulation.

### Comment l'implémenter ?

- Déterminez quelle classe jouera le rôle du créateur. Il est important de savoir si le programme utilise un objet central de ce type ou plusieurs objets plus petits.

- Créez la classe memento. Un par un, déclarez un ensemble de champs qui reflètent les champs déclarés à l'intérieur de la classe d'origine.

- Rendez la classe memento immuable. Un memento ne doit accepter les données qu'une seule fois, via le constructeur. La classe ne doit pas avoir de setters.

- Si votre langage de programmation prend en charge les classes imbriquées, imbriquez le mémento dans le créateur. Sinon, extrayez une interface vide de la classe memento et faites en sorte que tous les autres objets l'utilisent pour faire référence au memento. Vous pouvez ajouter des opérations de métadonnées à l'interface, mais rien qui expose l'état de l'expéditeur.

- Ajoutez une méthode pour produire des souvenirs à la classe d'origine. Le créateur doit transmettre son état au memento via un ou plusieurs arguments du constructeur du memento.

- Le type de retour de la méthode doit être celui de l'interface que vous avez extraite à l'étape précédente (en supposant que vous l'avez extraite du tout). Sous le capot, la méthode de production de mémento devrait fonctionner directement avec la classe memento.

- Ajoutez une méthode pour restaurer l'état de l'expéditeur dans sa classe. Il doit accepter un objet memento comme argument. Si vous avez extrait une interface à l'étape précédente, définissez-en le type du paramètre. Dans ce cas, vous devez transtyper l'objet entrant dans la classe memento, car l'expéditeur a besoin d'un accès complet à cet objet.

- Le gardien, qu'il représente un objet de commande, un historique ou quelque chose de complètement différent, doit savoir quand demander de nouveaux souvenirs à l'expéditeur, comment les stocker et quand restaurer l'expéditeur avec un souvenir particulier.

- Le lien entre les gardiens et les créateurs peut être déplacé dans la classe memento. Dans ce cas, chaque souvenir doit être connecté à l'auteur qui l'a créé. La méthode de restauration passerait également à la classe memento. Cependant, tout cela n'aurait de sens que si la classe memento est imbriquée dans originator ou si la classe originator fournit suffisamment de setters pour remplacer son état.

### Avantages :

- Vous pouvez produire des instantanés de l’état de l’objet sans violer son encapsulation.
- Vous pouvez simplifier le code de l'expéditeur en laissant le gardien conserver l'historique de l'état de l'expéditeur.

### Inconvénients :

- L'application peut consommer beaucoup de RAM si les clients créent trop souvent des souvenirs.
- Les gardiens doivent suivre le cycle de vie du créateur pour pouvoir détruire les souvenirs obsolètes.
- La plupart des langages de programmation dynamiques, tels que PHP, Python et JavaScript, ne peuvent garantir que l’état du memento reste intact.