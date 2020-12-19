# Design pattern : Proxy

Le proxy est un modèle de conception structurelle qui vous permet de fournir un substitut ou un espace réservé pour un autre objet. Un proxy contrôle l'accès à l'objet d'origine, vous permettant d'effectuer quelque chose avant ou après que la demande parvienne à l'objet d'origine.

### Ressources :

- https://refactoring.guru/design-patterns/proxy

### Problématiques :

Pourquoi voudriez-vous contrôler l'accès à un objet? Voici un exemple: vous avez un objet massif qui consomme une grande quantité de ressources système. Vous en avez besoin de temps en temps, mais pas toujours.

Vous pouvez implémenter une initialisation différée: créez cet objet uniquement lorsque cela est réellement nécessaire. Tous les clients de l’objet devraient exécuter un code d’initialisation différée. Malheureusement, cela entraînerait probablement beaucoup de duplication de code.

Dans un monde idéal, nous voudrions mettre ce code directement dans la classe de notre objet, mais ce n’est pas toujours possible. Par exemple, la classe peut faire partie d'une bibliothèque tierce fermée.

### Solution :

Le modèle Proxy vous suggère de créer une nouvelle classe de proxy avec la même interface qu'un objet de service d'origine. Ensuite, vous mettez à jour votre application afin qu'elle transmette l'objet proxy à tous les clients de l'objet d'origine. À la réception d'une demande d'un client, le proxy crée un véritable objet de service et lui délègue tout le travail.

Mais quel est l’avantage? Si vous avez besoin d'exécuter quelque chose avant ou après la logique principale de la classe, le proxy vous permet de le faire sans changer cette classe. Étant donné que le proxy implémente la même interface que la classe d'origine, il peut être passé à n'importe quel client qui attend un véritable objet de service.


### Quand est ce qu'il faut l'appliquer ?

- Initialisation paresseuse (proxy virtuel). C'est lorsque vous avez un objet de service lourd qui gaspille les ressources système en étant toujours actif, même si vous n'en avez besoin que de temps en temps.

- Contrôle d'accès (proxy de protection). C'est à ce moment que vous souhaitez que seuls des clients spécifiques puissent utiliser l'objet de service; par exemple, lorsque vos objets sont des éléments cruciaux d'un système d'exploitation et que les clients sont diverses applications lancées (y compris des applications malveillantes).

- Exécution locale d'un service distant (proxy distant). Cela se produit lorsque l'objet de service se trouve sur un serveur distant.

- Requêtes de journalisation (proxy de journalisation). C'est à ce moment que vous souhaitez conserver un historique des demandes adressées à l'objet de service.

- Mise en cache des résultats de la demande (proxy de mise en cache). C'est à ce moment que vous devez mettre en cache les résultats des demandes des clients et gérer le cycle de vie de ce cache, en particulier si les résultats sont assez volumineux.

- Référence intelligente. C'est à ce moment que vous devez être en mesure de rejeter un objet lourd une fois qu'aucun client ne l'utilise.


### Comment l'implémenter ?

- S'il n'y a pas d'interface de service préexistante, créez-en une pour rendre les objets proxy et service interchangeables. Il n’est pas toujours possible d’extraire l’interface de la classe de service, car vous devrez modifier tous les clients du service pour utiliser cette interface. Le plan B consiste à faire du proxy une sous-classe de la classe de service, et de cette façon il héritera de l'interface du service.

- Créez la classe proxy. Il doit avoir un champ pour stocker une référence au service. Habituellement, les mandataires créent et gèrent tout le cycle de vie de leurs services. En de rares occasions, un service est passé au proxy via un constructeur par le client.

- Implémentez les méthodes proxy en fonction de leurs objectifs. Dans la plupart des cas, après avoir effectué un certain travail, le proxy doit déléguer le travail à l'objet de service.

- Pensez à introduire une méthode de création qui décide si le client obtient un proxy ou un vrai service. Cela peut être une simple méthode statique dans la classe proxy ou une méthode d'usine à part entière.

- Envisagez d'implémenter une initialisation différée pour l'objet de service.


### Avantages :

- Vous pouvez contrôler l'objet de service sans que les clients le sachent.

- Vous pouvez gérer le cycle de vie de l'objet de service lorsque les clients ne s'en soucient pas.

- Le proxy fonctionne même si l'objet de service n'est pas prêt ou n'est pas disponible.

- Principe ouvert / fermé. Vous pouvez introduire de nouveaux proxys sans changer le service ou les clients.

### Inconvénients :

- Le code peut devenir plus compliqué car vous devez introduire de nombreuses nouvelles classes.
- La réponse du service peut être retardée.