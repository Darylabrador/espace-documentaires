# Design pattern : Mediator

Mediator est un modèle de conception comportementale qui vous permet de réduire les dépendances chaotiques entre les objets. Le modèle restreint les communications directes entre les objets et les oblige à collaborer uniquement via un objet médiateur. Il est aussi connu  sous le nom d'intermédiaire ou controller.

### Ressources :

- https://refactoring.guru/design-patterns/mediator

### Problématiques :

Supposons que vous ayez une boîte de dialogue pour créer et modifier les profils des clients. Il se compose de divers contrôles de formulaire tels que des champs de texte, des cases à cocher, des boutons, etc.

Certains des éléments du formulaire peuvent interagir avec d'autres. Par exemple, cocher la case "J'ai un chien" peut révéler un champ de texte caché pour saisir le nom du chien. Un autre exemple est le bouton d'envoi qui doit valider les valeurs de tous les champs avant d'enregistrer les données.

En ayant cette logique implémentée directement dans le code des éléments de formulaire, vous rendez les classes de ces éléments beaucoup plus difficiles à réutiliser dans d'autres formes de l'application. Par exemple, vous ne pourrez pas utiliser cette classe de case à cocher dans un autre formulaire, car elle est associée au champ de texte du chien. Vous pouvez utiliser soit toutes les classes impliquées dans le rendu du formulaire de profil, soit aucune du tout.

### Solution :

Le modèle Mediator suggère que vous devez cesser toute communication directe entre les composants que vous souhaitez rendre indépendants les uns des autres. Au lieu de cela, ces composants doivent collaborer indirectement, en appelant un objet médiateur spécial qui redirige les appels vers les composants appropriés. En conséquence, les composants ne dépendent que d'une seule classe de médiateur au lieu d'être couplés à des dizaines de leurs collègues.

Dans notre exemple avec le formulaire d'édition de profil, la classe de dialogue elle-même peut jouer le rôle de médiateur. Très probablement, la classe de dialogue connaît déjà tous ses sous-éléments, vous n'aurez donc même pas besoin d'introduire de nouvelles dépendances dans cette classe.

Le changement le plus significatif concerne les éléments de formulaire réels. Examinons le bouton d'envoi. Auparavant, chaque fois qu'un utilisateur cliquait sur le bouton, il devait valider les valeurs de tous les éléments de formulaire individuels. Maintenant, son seul travail est d'avertir la boîte de dialogue du clic. À la réception de cette notification, la boîte de dialogue effectue elle-même les validations ou transmet la tâche aux éléments individuels. Ainsi, au lieu d'être lié à une dizaine d'éléments de formulaire, le bouton ne dépend que de la classe de dialogue.

Vous pouvez aller plus loin et rendre la dépendance encore plus lâche en extrayant l'interface commune pour tous les types de dialogues. L'interface déclarerait la méthode de notification que tous les éléments de formulaire peuvent utiliser pour notifier la boîte de dialogue des événements qui se produisent sur ces éléments. Ainsi, notre bouton d'envoi devrait désormais pouvoir fonctionner avec n'importe quelle boîte de dialogue implémentant cette interface.

De cette façon, le modèle Mediator vous permet d'encapsuler un réseau complexe de relations entre divers objets à l'intérieur d'un seul objet médiateur. Moins une classe a de dépendances, plus il devient facile de modifier, d'étendre ou de réutiliser cette classe.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Mediator lorsqu'il est difficile de changer certaines des classes car elles sont étroitement associées à un tas d'autres classes.
- Utilisez le modèle lorsque vous ne pouvez pas réutiliser un composant dans un autre programme car il dépend trop d’autres composants.
- Utilisez le médiateur lorsque vous créez des tonnes de sous-classes de composants juste pour réutiliser un comportement de base dans divers contextes.

### Comment l'implémenter ?

- Identifiez un groupe de classes étroitement couplées qui gagneraient à être plus indépendantes (par exemple, pour une maintenance plus facile ou une réutilisation plus simple de ces classes).

- Déclarez l'interface du médiateur et décrivez le protocole de communication souhaité entre les médiateurs et divers composants. Dans la plupart des cas, une seule méthode de réception des notifications des composants est suffisante.

- Cette interface est cruciale lorsque vous souhaitez réutiliser des classes de composants dans différents contextes. Tant que le composant fonctionne avec son médiateur via l'interface générique, vous pouvez lier le composant à une implémentation différente du médiateur.

- Implémentez la classe de médiateur concret. Cette classe gagnerait à stocker des références à tous les composants qu'elle gère.
    Vous pouvez aller encore plus loin et rendre le médiateur responsable de la création et de la destruction des objets composants. Après cela, le médiateur peut ressembler à une usine ou à une façade.
    Les composants doivent stocker une référence à l'objet médiateur. La connexion est généralement établie dans le constructeur du composant, où un objet médiateur est passé en argument.

- Modifiez le code des composants afin qu'ils appellent la méthode de notification du médiateur au lieu des méthodes des autres composants. Extrayez le code qui implique l'appel d'autres composants dans la classe médiateur. Exécutez ce code chaque fois que le médiateur reçoit des notifications de ce composant.

### Avantages :

- Principe de responsabilité unique. Vous pouvez extraire les communications entre divers composants en un seul endroit, ce qui facilite leur compréhension et leur maintenance.
- Principe ouvert / fermé. Vous pouvez introduire de nouveaux médiateurs sans avoir à modifier les composants réels.
- Vous pouvez réduire le couplage entre les différents composants d'un programme.
- Vous pouvez réutiliser des composants individuels plus facilement.

### Inconvénients :

- Au fil du temps, un médiateur peut évoluer en un <a href="https://en.wikipedia.org/wiki/God_object">objet divin</a>