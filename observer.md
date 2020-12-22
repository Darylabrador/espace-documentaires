# Design pattern : Observer

Observer est un modèle de conception comportementale qui vous permet de définir un mécanisme d'abonnement pour informer plusieurs objets de tout événement survenant à l'objet qu'ils observent. Il est aussi connu sous le nom de Event-Subscriber ou Listener.

### Ressources :

- https://refactoring.guru/design-patterns/observer

### Problématiques :

Imaginez que vous ayez deux types d'objets: un client et un magasin. Le client est très intéressé par une marque de produit en particulier (par exemple, c'est un nouveau modèle d'iPhone) qui devrait être disponible dans le magasin très prochainement.

Le client pouvait visiter le magasin tous les jours et vérifier la disponibilité des produits. Mais tant que le produit est encore en route, la plupart de ces voyages seraient inutiles.

D'autre part, le magasin pourrait envoyer des tonnes d'e-mails (qui pourraient être considérés comme du spam) à tous les clients chaque fois qu'un nouveau produit devient disponible. Cela éviterait à certains clients des voyages interminables vers le magasin. Dans le même temps, cela a dérangé d'autres clients qui ne sont pas intéressés par les nouveaux produits.

Il semble que nous ayons un conflit. Soit le client perd du temps à vérifier la disponibilité des produits, soit le magasin gaspille des ressources à notifier les mauvais clients.

### Solution :

L'objet qui a un état intéressant est souvent appelé sujet, mais comme il va également informer les autres objets des modifications apportées à son état, nous l'appellerons éditeur. Tous les autres objets qui souhaitent suivre les modifications apportées à l'état de l'éditeur sont appelés abonnés.

Le modèle Observer suggère que vous ajoutiez un mécanisme d'abonnement à la classe d'éditeur afin que les objets individuels puissent s'abonner ou se désabonner d'un flux d'événements provenant de cet éditeur. N'aie pas peur! Tout n’est pas aussi compliqué qu’il y paraît. 

En réalité, ce mécanisme consiste en 
    1) un champ de tableau pour stocker une liste de références aux objets abonnés
    2) plusieurs méthodes publiques qui permettent d'ajouter des abonnés et de les supprimer de cette liste.

Désormais, chaque fois qu'un événement important arrive à l'éditeur, il passe au-dessus de ses abonnés et appelle la méthode de notification spécifique sur leurs objets.

Les applications réelles peuvent avoir des dizaines de classes d'abonnés différentes qui souhaitent suivre les événements de la même classe d'éditeurs. Vous ne voudriez pas associer l'éditeur à toutes ces classes. En outre, vous ne connaissez peut-être même pas certains d'entre eux à l'avance si votre classe d'éditeur est censée être utilisée par d'autres personnes. C’est pourquoi il est essentiel que tous les abonnés mettent en œuvre la même interface et que l’éditeur communique avec eux uniquement via cette interface. Cette interface doit déclarer la méthode de notification avec un ensemble de paramètres que l'éditeur peut utiliser pour transmettre des données contextuelles avec la notification.

Si votre application dispose de plusieurs types d'éditeurs différents et que vous souhaitez rendre vos abonnés compatibles avec tous, vous pouvez aller encore plus loin et faire en sorte que tous les éditeurs suivent la même interface. Cette interface n'aurait besoin que de décrire quelques méthodes d'abonnement. L'interface permettrait aux abonnés d'observer les états des éditeurs sans se coupler à leurs classes concrètes.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Observer lorsque les modifications de l'état d'un objet peuvent nécessiter la modification d'autres objets et que l'ensemble réel d'objets est inconnu au préalable ou change de manière dynamique.

- Utilisez le modèle lorsque certains objets de votre application doivent en observer d'autres, mais uniquement pendant une durée limitée ou dans des cas spécifiques.

### Comment l'implémenter ?

- Examinez votre logique métier et essayez de la décomposer en deux parties: la fonctionnalité de base, indépendante des autres codes, agira en tant qu'éditeur; le reste se transformera en un ensemble de classes d'abonnés.

- Déclarez l'interface abonné. Au strict minimum, il devrait déclarer une seule méthode de mise à jour.

- Déclarez l'interface de l'éditeur et décrivez une paire de méthodes pour ajouter et supprimer un objet abonné de la liste. N'oubliez pas que les éditeurs doivent travailler avec les abonnés uniquement via l'interface abonné.

- Décidez où placer la liste d'abonnement réelle et la mise en œuvre des méthodes d'abonnement. Habituellement, ce code a le même aspect pour tous les types d'éditeurs, de sorte que l'endroit évident pour le mettre est dans une classe abstraite dérivée directement de l'interface de l'éditeur. Les éditeurs concrets étendent cette classe, héritant du comportement d'abonnement. Cependant, si vous appliquez le modèle à une hiérarchie de classes existante, envisagez une approche basée sur la composition: placez la logique d'abonnement dans un objet séparé et faites en sorte que tous les vrais éditeurs l'utilisent.

- Créez des classes d'éditeurs concrètes. Chaque fois que quelque chose d'important se produit chez un éditeur, il doit en informer tous ses abonnés.

- Implémentez les méthodes de notification de mise à jour dans des classes d'abonnés concrètes. La plupart des abonnés auraient besoin de données contextuelles sur l'événement. Il peut être passé comme argument de la méthode de notification. Mais il y a une autre option. À la réception d'une notification, l'abonné peut récupérer toutes les données directement à partir de la notification. Dans ce cas, l'éditeur doit se passer par la méthode de mise à jour. L'option la moins flexible consiste à lier un éditeur à l'abonné en permanence via le constructeur.

- Le client doit créer tous les abonnés nécessaires et les enregistrer auprès des éditeurs appropriés.

### Avantages :

- Principe ouvert / fermé. Vous pouvez introduire de nouvelles classes d'abonnés sans avoir à modifier le code de l'éditeur (et inversement s'il existe une interface éditeur).
- Vous pouvez établir des relations entre les objets lors de l'exécution.

### Inconvénients :

- Les abonnés sont notifiés dans un ordre aléatoire.