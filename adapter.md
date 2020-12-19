# Design pattern : Adapter

Le patern design adapter est aussi connu sous le nom de "Wrapper". Il s'agit ici d'un modle de conception structurelle qui permet aux objets avec des interfaces incompatobles de collaborer.

### Ressources :

- https://refactoring.guru/design-patterns/adapter

### Problématiques :

Imaginez que vous créez une application de surveillance boursière. L'application télécharge les données boursières de plusieurs sources au format XML, puis affiche de jolis graphiques et diagrammes pour l'utilisateur. À un moment donné, vous décidez d'améliorer l'application en intégrant une bibliothèque d'analyse tierce intelligente. Mais il y a un hic: la bibliothèque d'analyse ne fonctionne qu'avec des données au format JSON.

Vous pouvez modifier la bibliothèque pour qu'elle fonctionne avec XML. Cependant, cela peut casser du code existant qui repose sur la bibliothèque. Et pire, vous n’avez peut-être pas accès au code source de la bibliothèque en premier lieu, ce qui rend cette approche impossible.

### Solution :

Vous pouvez créer un adaptateur. Il s'agit d'un objet spécial qui convertit l'interface d'un objet afin qu'un autre objet puisse le comprendre. Un adaptateur enveloppe l'un des objets pour masquer la complexité de la conversion qui se produit dans les coulisses. L'objet encapsulé ne connaît même pas l'adaptateur. Par exemple, vous pouvez envelopper un objet qui fonctionne en mètres et en kilomètres avec un adaptateur qui convertit toutes les données en unités impériales telles que les pieds et les miles.

Les adaptateurs peuvent non seulement convertir les données en différents formats, mais peuvent également aider les objets avec différentes interfaces à collaborer. Voici comment ça fonctionne:

- L'adaptateur obtient une interface, compatible avec l'un des objets existants.
- Grâce à cette interface, l’objet existant peut appeler en toute sécurité les méthodes de l’adaptateur.
- À la réception d'un appel, l'adaptateur transmet la demande au deuxième objet, mais dans un format et dans l'ordre que le deuxième objet attend.

Parfois, il est même possible de créer un adaptateur bidirectionnel capable de convertir les appels dans les deux sens.

Revenons à notre application boursière. Pour résoudre le dilemme des formats incompatibles, vous pouvez créer des adaptateurs XML vers JSON pour chaque classe de la bibliothèque d'analyse avec laquelle votre code fonctionne directement. Ensuite, vous ajustez votre code pour communiquer avec la bibliothèque uniquement via ces adaptateurs. Lorsqu'un adaptateur reçoit un appel, il traduit les données XML entrantes en une structure JSON et passe l'appel aux méthodes appropriées d'un objet d'analyse encapsulé.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez la classe Adapter lorsque vous souhaitez utiliser une classe existante, mais que son interface n'est pas compatible avec le reste de votre code.
- Utilisez le modèle lorsque vous souhaitez réutiliser plusieurs sous-classes existantes qui ne disposent pas de fonctionnalités communes qui ne peuvent pas être ajoutées à la superclasse.

### Comment l'implémenter ?

- Assurez-vous que vous avez au moins deux classes avec des interfaces incompatibles:
        Une classe de service utile, que vous ne pouvez pas modifier (souvent tierce, héritée ou avec de nombreuses dépendances existantes).
        Une ou plusieurs classes de clients qui bénéficieraient de l'utilisation de la classe de service.

- Déclarez l'interface client et décrivez comment les clients communiquent avec le service.

- Créez la classe d'adaptateur et faites-la suivre l'interface client. Laissez toutes les méthodes vides pour le moment.

- Ajoutez un champ à la classe d'adaptateur pour stocker une référence à l'objet de service. La pratique courante consiste à initialiser ce champ via le constructeur, mais il est parfois plus pratique de le transmettre à l’adaptateur lors de l’appel de ses méthodes.

- Une par une, implémentez toutes les méthodes de l'interface client dans la classe adaptateur. L'adaptateur doit déléguer la plupart du travail réel à l'objet de service, en ne gérant que l'interface ou la conversion de format de données.

- Les clients doivent utiliser l'adaptateur via l'interface client. Cela vous permettra de modifier ou d'étendre les adaptateurs sans affecter le code client.


### Avantages :

- Principe de responsabilité unique. Vous pouvez séparer l'interface ou le code de conversion de données de la logique métier principale du programme.
- Principe ouvert / fermé. Vous pouvez introduire de nouveaux types d'adaptateurs dans le programme sans casser le code client existant, à condition qu'ils fonctionnent avec les adaptateurs via l'interface client.

### Inconvénients :

- La complexité globale du code augmente car vous devez introduire un ensemble de nouvelles interfaces et classes. Parfois, il est plus simple de modifier simplement la classe de service afin qu’elle corresponde au reste de votre code.

