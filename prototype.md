# Design pattern : Prototype

Le prototype aussi connue sous le nom de "clone" est un modèle de conception créative qui permet de copier des objets existants sans rendre le code dépendant de leurs classes.

### Ressources :

- https://refactoring.guru/design-patterns/prototype

### Problématiques :

Supposons que vous ayez un objet et que vous souhaitiez en créer une copie exacte. Comment feriez-vous cela? Tout d'abord, vous devez créer un nouvel objet de la même classe. Ensuite, vous devez parcourir tous les champs de l'objet d'origine et copier leurs valeurs dans le nouvel objet.

Agréable! Mais il y a un hic. Tous les objets ne peuvent pas être copiés de cette manière car certains des champs de l’objet peuvent être privés et ne pas être visibles de l’extérieur de l’objet lui-même.

Il y a un autre problème avec l’approche directe. Puisque vous devez connaître la classe de l'objet pour créer un doublon, votre code devient dépendant de cette classe. Si la dépendance supplémentaire ne vous fait pas peur, il y a un autre problème. Parfois, vous ne connaissez que l'interface que suit l'objet, mais pas sa classe concrète, lorsque, par exemple, un paramètre dans une méthode accepte des objets qui suivent une interface.

### Solution :

Le modèle Prototype délègue le processus de clonage aux objets réels qui sont clonés. Le modèle déclare une interface commune pour tous les objets prenant en charge le clonage. Cette interface vous permet de cloner un objet sans coupler votre code à la classe de cet objet. Habituellement, une telle interface ne contient qu'une seule méthode de clonage.

L'implémentation de la méthode clone est très similaire dans toutes les classes. La méthode crée un objet de la classe actuelle et reporte toutes les valeurs de champ de l'ancien objet dans le nouveau. Vous pouvez même copier des champs privés car la plupart des langages de programmation permettent aux objets d'accéder aux champs privés d'autres objets appartenant à la même classe.

Un objet qui prend en charge le clonage est appelé un prototype. Lorsque vos objets ont des dizaines de champs et des centaines de configurations possibles, leur clonage peut servir d'alternative au sous-classement.

Voici comment cela fonctionne: vous créez un ensemble d’objets, configurés de différentes manières. Lorsque vous avez besoin d’un objet comme celui que vous avez configuré, il vous suffit de cloner un prototype au lieu de créer un nouvel objet à partir de zéro.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Prototype lorsque votre code ne doit pas dépendre des classes concrètes d’objets que vous devez copier.

- Utilisez le modèle lorsque vous souhaitez réduire le nombre de sous-classes qui ne diffèrent que par la manière dont elles initialisent leurs objets respectifs. Quelqu'un aurait pu créer ces sous-classes pour pouvoir créer des objets avec une configuration spécifique.

### Comment l'implémenter ?


- Créez l'interface prototype et déclarez-y la méthode de clonage. Ou ajoutez simplement la méthode à toutes les classes d'une hiérarchie de classes existante, si vous en avez une.

- Une classe prototype doit définir le constructeur alternatif qui accepte un objet de cette classe comme argument. Le constructeur doit copier les valeurs de tous les champs définis dans la classe de l'objet passé dans l'instance nouvellement créée. Si vous modifiez une sous-classe, vous devez appeler le constructeur parent pour laisser la superclasse gérer le clonage de ses champs privés.

- Si votre langage de programmation ne prend pas en charge la surcharge de méthode, vous pouvez définir une méthode spéciale pour copier les données d’objet. Le constructeur est un endroit plus pratique pour ce faire, car il fournit l'objet résultant juste après avoir appelé l'opérateur new.

- La méthode de clonage consiste généralement en une seule ligne: exécuter un nouvel opérateur avec la version prototypique du constructeur. Notez que chaque classe doit remplacer explicitement la méthode de clonage et utiliser son propre nom de classe avec le nouvel opérateur. Sinon, la méthode de clonage peut produire un objet d'une classe parent.

- Vous pouvez éventuellement créer un registre de prototypes centralisé pour stocker un catalogue de prototypes fréquemment utilisés.

- Vous pouvez implémenter le registre en tant que nouvelle classe d'usine ou le placer dans la classe prototype de base avec une méthode statique pour récupérer le prototype. Cette méthode doit rechercher un prototype en fonction de critères de recherche que le code client transmet à la méthode. Les critères peuvent être une simple balise de chaîne ou un ensemble complexe de paramètres de recherche. Une fois le prototype approprié trouvé, le registre doit le cloner et renvoyer la copie au client.

- Enfin, remplacez les appels directs aux constructeurs des sous-classes par des appels à la méthode factory du registre prototype.


### Avantages :

- Vous pouvez cloner des objets sans les coupler à leurs classes concrètes.
- Vous pouvez vous débarrasser du code d'initialisation répété en faveur du clonage de prototypes prédéfinis.
- Vous pouvez produire des objets complexes plus facilement.
- Vous obtenez une alternative à l'héritage lorsque vous traitez des préréglages de configuration pour des objets complexes.

### Inconvénients :

-  Le clonage d'objets complexes ayant des références circulaires peut être très délicat.