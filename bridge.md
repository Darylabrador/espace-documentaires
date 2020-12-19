# Design pattern : Bridge

Bridge est un modèle de conception structurelle qui vous permet de diviser une grande classe ou un ensemble de classes étroitement liées en deux hiérarchies distinctes (abstraction et implémentation) qui peuvent être développées indépendamment l'une de l'autre.

### Ressources :

- https://refactoring.guru/design-patterns/bridge

### Problématiques :

Supposons que vous ayez une classe Shape géométrique avec une paire de sous-classes: Circle et Square. Vous souhaitez étendre cette hiérarchie de classes pour incorporer des couleurs, vous prévoyez donc de créer des sous-classes de formes rouges et bleues. Cependant, comme vous avez déjà deux sous-classes, vous devrez créer quatre combinaisons de classes telles que BlueCircle et RedSquare. L'ajout de nouveaux types de formes et de couleurs à la hiérarchie la fera croître de manière exponentielle. Par exemple, pour ajouter une forme de triangle, vous devez introduire deux sous-classes, une pour chaque couleur. Et après cela, l'ajout d'une nouvelle couleur nécessiterait la création de trois sous-classes, une pour chaque type de forme. Plus on avance, plus ça empire.

### Solution :

Ce problème se produit car nous essayons d'étendre les classes de formes dans deux dimensions indépendantes: par forme et par couleur. C'est un problème très courant avec l'héritage de classe. Le modèle Bridge tente de résoudre ce problème en passant de l'héritage à la composition de l'objet. Cela signifie que vous extrayez l'une des dimensions dans une hiérarchie de classes distincte, de sorte que les classes d'origine référencent un objet de la nouvelle hiérarchie, au lieu d'avoir tous ses états et comportements dans une classe. En suivant cette approche, nous pouvons extraire le code lié à la couleur dans sa propre classe avec deux sous-classes: Rouge et Bleu. La classe Shape obtient alors un champ de référence pointant vers l'un des objets couleur. Désormais, la forme peut déléguer tout travail lié à la couleur à l'objet couleur lié. Cette référence agira comme un pont entre les classes Shape et Color. À partir de maintenant, l'ajout de nouvelles couleurs ne nécessitera pas de modifier la hiérarchie des formes, et vice versa.

#### Abstraction and Implementation

L'abstraction (également appelée interface) est une couche de contrôle de haut niveau pour certaines entités. Ce calque n’est pas censé faire un vrai travail tout seul. Il doit déléguer le travail à la couche d'implémentation (également appelée plateforme). Lorsqu'on parle d'applications réelles, l'abstraction peut être représentée par une interface utilisateur graphique (GUI), et l'implémentation peut être le code du système d'exploitation (API) sous-jacent que la couche GUI appelle en réponse aux interactions des utilisateurs.

De manière générale, vous pouvez étendre une telle application dans deux directions indépendantes:

- Avoir plusieurs interfaces graphiques différentes (par exemple, conçues pour les clients réguliers ou les administrateurs).
- Prend en charge plusieurs API différentes (par exemple, pour pouvoir lancer l'application sous Windows, Linux et macOS).

L'objet d'abstraction contrôle l'apparence de l'application, déléguant le travail réel à l'objet d'implémentation lié. Les différentes implémentations sont interchangeables tant qu'elles suivent une interface commune, permettant à la même interface graphique de fonctionner sous Windows et Linux. Par conséquent, vous pouvez modifier les classes GUI sans toucher aux classes liées à l'API. De plus, l'ajout de la prise en charge d'un autre système d'exploitation nécessite uniquement la création d'une sous-classe dans la hiérarchie d'implémentation.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Bridge lorsque vous souhaitez diviser et organiser une classe monolithique qui a plusieurs variantes de certaines fonctionnalités (par exemple, si la classe peut fonctionner avec différents serveurs de base de données).
- Utilisez le pattenr lorsque vous devez étendre une classe dans plusieurs dimensions orthogonales (indépendantes).
- Utilisez le Bridge si vous avez besoin de pouvoir changer d'implémentation au moment de l'exécution.


### Comment l'implémenter ?

- Identifiez les dimensions orthogonales dans vos classes. Ces concepts indépendants peuvent être: abstraction / plateforme, domaine / infrastructure, front-end / back-end, ou interface / implémentation.

- Découvrez les opérations dont le client a besoin et définissez-les dans la classe d'abstraction de base.

- Déterminez les opérations disponibles sur toutes les plateformes. Déclarez ceux dont l'abstraction a besoin dans l'interface d'implémentation générale.

- Pour toutes les plates-formes de votre domaine, créez des classes d'implémentation concrètes, mais assurez-vous qu'elles suivent toutes l'interface d'implémentation.

- Dans la classe d'abstraction, ajoutez un champ de référence pour le type d'implémentation. L'abstraction délègue la majeure partie du travail à l'objet d'implémentation référencé dans ce champ.

- Si vous disposez de plusieurs variantes de logique de haut niveau, créez des abstractions raffinées pour chaque variante en étendant la classe d'abstraction de base.

- Le code client doit passer un objet d'implémentation au constructeur de l'abstraction pour l'associer l'un à l'autre. Après cela, le client peut oublier l'implémentation et travailler uniquement avec l'objet d'abstraction.


### Avantages :

- Vous pouvez créer des classes et des applications indépendantes de la plate-forme. Le code client fonctionne avec des abstractions de haut niveau. Il n'est pas exposé aux détails de la plate-forme.
- Principe ouvert / fermé. Vous pouvez introduire de nouvelles abstractions et implémentations indépendamment les unes des autres.
- Principe de responsabilité unique. Vous pouvez vous concentrer sur la logique de haut niveau dans l'abstraction et sur les détails de la plate-forme dans l'implémentation.

### Inconvénients :

- Vous pouvez rendre le code plus compliqué en appliquant le modèle à une classe hautement cohésive.