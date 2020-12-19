# Design pattern : Decorator

Decorator est un modèle de conception structurelle qui vous permet d'attacher de nouveaux comportements à des objets en plaçant ces objets dans des objets wrapper spéciaux contenant les comportements.

### Ressources :

- https://refactoring.guru/design-patterns/decorator

### Problématiques :

Imaginez que vous travaillez sur une bibliothèque de notifications qui permet à d'autres programmes d'informer leurs utilisateurs des événements importants.

La version initiale de la bibliothèque était basée sur la classe Notifier qui ne contenait que quelques champs, un constructeur et une seule méthode d'envoi. La méthode peut accepter un argument de message d'un client et envoyer le message à une liste d'e-mails qui ont été transmis au notificateur via son constructeur. Une application tierce qui agissait en tant que client était censée créer et configurer l'objet de notification une fois, puis l'utiliser chaque fois qu'un événement important se produisait.

À un moment donné, vous réalisez que les utilisateurs de la bibliothèque attendent plus que de simples notifications par courrier électronique. Beaucoup d'entre eux aimeraient recevoir un SMS sur des problèmes critiques. D'autres aimeraient être informés sur Facebook et, bien sûr, les utilisateurs professionnels aimeraient recevoir des notifications Slack.

A quel point cela peut-il être difficile? Vous avez étendu la classe Notifier et placé les méthodes de notification supplémentaires dans de nouvelles sous-classes. Maintenant, le client était censé instancier la classe de notification souhaitée et l'utiliser pour toutes les notifications ultérieures.

Mais quelqu'un vous a raisonnablement demandé: «Pourquoi ne pouvez-vous pas utiliser plusieurs types de notification à la fois? Si votre maison est en feu, vous voudrez probablement être informé via tous les canaux. Vous avez essayé de résoudre ce problème en créant des sous-classes spéciales qui combinaient plusieurs méthodes de notification au sein d'une même classe. Cependant, il est rapidement devenu évident que cette approche gonflerait énormément le code, non seulement le code de la bibliothèque, mais également le code du client.


### Solution :

L’extension d’une classe est la première chose qui vous vient à l’esprit lorsque vous devez modifier le comportement d’un objet. Cependant, l'héritage comporte plusieurs mises en garde sérieuses dont vous devez être conscient. L'héritage est statique. Vous ne pouvez pas modifier le comportement d’un objet existant lors de l’exécution. Vous ne pouvez remplacer l’objet entier que par un autre créé à partir d’une sous-classe différente.
Les sous-classes ne peuvent avoir qu'une seule classe parente. Dans la plupart des langages, l'héritage ne permet pas à une classe d'hériter des comportements de plusieurs classes en même temps.

L'un des moyens de surmonter ces mises en garde consiste à utiliser l'agrégation ou la composition au lieu de l'héritage. Les deux alternatives fonctionnent presque de la même manière: un objet a une référence à un autre et lui délègue du travail, alors qu'avec l'héritage, l'objet lui-même est capable de faire ce travail, héritant du comportement de sa superclasse.

Avec cette nouvelle approche, vous pouvez facilement remplacer l'objet «assistant» lié par un autre, en modifiant le comportement du conteneur lors de l'exécution. Un objet peut utiliser le comportement de différentes classes, ayant des références à plusieurs objets et leur déléguant toutes sortes de travaux. L'agrégation / composition est le principe clé de nombreux modèles de conception, y compris Decorator.

«Wrapper» est le surnom alternatif du motif Decorator qui exprime clairement l'idée principale du motif. Un wrapper est un objet qui peut être lié à un objet cible. L'encapsuleur contient le même ensemble de méthodes que la cible et lui délègue toutes les demandes qu'il reçoit. Toutefois, le wrapper peut modifier le résultat en effectuant quelque chose avant ou après avoir transmis la demande à la cible.

Quand un simple emballage devient-il le véritable décorateur? Comme je l'ai mentionné, le wrapper implémente la même interface que l'objet enveloppé. C’est pourquoi du point de vue du client, ces objets sont identiques. Faites en sorte que le champ de référence de l'encapsuleur accepte tout objet qui suit cette interface. Cela vous permettra de couvrir un objet dans plusieurs wrappers, en y ajoutant le comportement combiné de tous les wrappers.


### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Decorator lorsque vous avez besoin de pouvoir attribuer des comportements supplémentaires aux objets au moment de l'exécution sans casser le code qui utilise ces objets.
- Utilisez le modèle lorsqu'il est difficile ou impossible d'étendre le comportement d'un objet à l'aide de l'héritage.

### Comment l'implémenter ?

- Assurez-vous que votre domaine d'entreprise peut être représenté comme un composant principal avec plusieurs couches facultatives dessus.

- Déterminez quelles méthodes sont communes au composant principal et aux couches facultatives. Créez une interface de composant et déclarez-y ces méthodes.

- Créez une classe de composants concrets et définissez-y le comportement de base.

- Créez une classe de décorateur de base. Il doit avoir un champ pour stocker une référence à un objet encapsulé. Le champ doit être déclaré avec le type d'interface de composant pour permettre la liaison aux composants en béton ainsi qu'aux décorateurs. Le décorateur de base doit déléguer tout le travail à l'objet encapsulé.

- Assurez-vous que toutes les classes implémentent l'interface du composant.

- Créez des décorateurs en béton en les prolongeant du décorateur de base. Un décorateur concret doit exécuter son comportement avant ou après l'appel à la méthode parent (qui délègue toujours à l'objet encapsulé).

- Le code client doit être responsable de la création des décorateurs et de leur composition selon les besoins du client.

### Avantages :

- Vous pouvez étendre le comportement d’un objet sans créer de nouvelle sous-classe.
- Vous pouvez ajouter ou supprimer des responsabilités d'un objet lors de l'exécution.
- Vous pouvez combiner plusieurs comportements en enveloppant un objet dans plusieurs décorateurs.
- Principe de responsabilité unique. Vous pouvez diviser une classe monolithique qui implémente de nombreuses variantes de comportement possibles en plusieurs classes plus petites.

### Inconvénients :

- Il est difficile de supprimer un wrapper spécifique de la pile de wrappers.
- Il est difficile de mettre en œuvre un décorateur de telle sorte que son comportement ne dépende pas de l’ordre dans la pile des décorateurs.
- Le code de configuration initial des couches peut sembler assez laid.