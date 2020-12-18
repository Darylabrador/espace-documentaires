# Design pattern : Builder

Il s'agit ici d'un modèle de conception créative qui permet de construire des objets complexes étape par étape. Ce modèle permet de produire différents types et représentations d'un objet en utilisant le même code de construction.

### Ressources :

- https://refactoring.guru/design-patterns/builder

### Problématiques :

Imaginez un objet complexe qui nécessite une initialisation laborieuse et étape par étape de nombreux champs et objets imbriqués. Un tel code d'initialisation est généralement enfoui dans un constructeur monstrueux avec de nombreux paramètres. Ou pire encore: dispersé dans tout le code client.

Par exemple, réfléchissons à la manière de créer un objet Maison. Pour construire une maison simple, vous devez construire quatre murs et un sol, installer une porte, installer une paire de fenêtres et construire un toit. Mais que se passe-t-il si vous voulez une maison plus grande et plus lumineuse, avec une cour arrière et d'autres avantages (comme un système de chauffage, la plomberie et le câblage électrique)?

La solution la plus simple consiste à étendre la classe Maison de base et à créer un ensemble de sous-classes pour couvrir toutes les combinaisons de paramètres. Mais finalement vous vous retrouverez avec un nombre considérable de sous-classes. Tout nouveau paramètre, tel que le style du porche, nécessitera de développer encore plus cette hiérarchie. Il existe une autre approche qui n'implique pas de sélection de sous-classes. Vous pouvez créer un constructeur géant directement dans la classe Maison de base avec tous les paramètres possibles qui contrôlent l'objet maison. Bien que cette approche élimine effectivement le besoin de sous-classes, elle crée un autre problème.

Dans la plupart des cas, la plupart des paramètres seront inutilisés, ce qui rend les appels du constructeur assez moche. Par exemple, seule une fraction des maisons possède des piscines, de sorte que les paramètres liés aux piscines seront inutiles neuf fois sur dix.


### Solution :

Imaginez un objet complexe qui nécessite une initialisation laborieuse et étape par étape de nombreux champs et objets imbriqués. Un tel code d'initialisation est généralement enfoui dans un constructeur monstrueux avec de nombreux paramètres. Ou pire encore: dispersé dans tout le code client.

Le modèle Builder vous suggère d'extraire le code de construction d'objet de sa propre classe et de le déplacer vers des objets séparés appelés générateurs.

Le modèle organise la construction d'objet en un ensemble d'étapes (buildWalls, buildDoor, etc.). Pour créer un objet, vous exécutez une série de ces étapes sur un objet générateur. L'important est que vous n'avez pas besoin d'appeler toutes les étapes. Vous ne pouvez appeler que les étapes nécessaires à la production d'une configuration particulière d'un objet.

Certaines des étapes de construction peuvent nécessiter une implémentation différente lorsque vous devez créer diverses représentations du produit. Par exemple, les murs d'une cabane peuvent être construits en bois, mais les murs du château doivent être construits en pierre.

Dans ce cas, vous pouvez créer plusieurs classes de générateur différentes qui implémentent le même ensemble d'étapes de construction, mais d'une manière différente. Ensuite, vous pouvez utiliser ces générateurs dans le processus de construction (c'est-à-dire un ensemble ordonné d'appels aux étapes de construction) pour produire différents types d'objets.

Par exemple, imaginez un constructeur qui construit tout à partir de bois et de verre, un deuxième qui construit tout avec de la pierre et du fer et un troisième qui utilise de l'or et des diamants. En appelant le même escalier, vous obtenez une maison ordinaire du premier constructeur, un petit château du deuxième et un palais du troisième. Cependant, cela ne fonctionnera que si le code client qui appelle les étapes de création est capable d'interagir avec les générateurs à l'aide d'une interface commune.

Director :

Vous pouvez aller plus loin et extraire une série d'appels aux étapes du générateur que vous utilisez pour construire un produit dans une classe distincte appelée director. La classe director définit l'ordre dans lequel exécuter les étapes de construction, tandis que le générateur fournit l'implémentation de ces étapes.


Il n’est pas strictement nécessaire d’avoir une classe de réalisateur dans votre programme. Vous pouvez toujours appeler les étapes de construction dans un ordre spécifique directement à partir du code client. Cependant, la classe de réalisateur peut être un bon endroit pour mettre diverses routines de construction afin que vous puissiez les réutiliser dans votre programme.

En outre, la classe de directeur masque complètement les détails de la construction du produit du code client. Le client n'a qu'à associer un constructeur à un directeur, lancer la construction avec le directeur et obtenir le résultat du constructeur.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Builder pour vous débarrasser d'un «constructeur télescopique».
- Utilisez le modèle Builder lorsque vous souhaitez que votre code puisse créer différentes représentations d'un produit (par exemple, des maisons en pierre et en bois).
- 1Utilisez le générateur pour créer des arbres composites ou d'autres objets complexes.

### Comment l'implémenter ?

- Assurez-vous de pouvoir définir clairement les étapes de construction courantes pour créer toutes les représentations de produits disponibles. Sinon, vous ne pourrez pas poursuivre la mise en œuvre du modèle.

- Déclarez ces étapes dans l'interface du générateur de base.

- Créez une classe de générateur concret pour chacune des représentations de produit et implémentez leurs étapes de construction.

- N'oubliez pas de mettre en œuvre une méthode pour récupérer le résultat de la construction. La raison pour laquelle cette méthode ne peut pas être déclarée dans l’interface du générateur est que divers générateurs peuvent créer des produits qui n’ont pas d’interface commune. Par conséquent, vous ne savez pas quel serait le type de retour pour une telle méthode. Cependant, si vous traitez des produits d'une seule hiérarchie, la méthode de récupération peut être ajoutée en toute sécurité à l'interface de base.

- Pensez à créer une classe de réalisateur. Il peut encapsuler différentes manières de construire un produit en utilisant le même objet constructeur.

- Le code client crée à la fois les objets générateur et directeur. Avant le début de la construction, le client doit transmettre un objet constructeur au directeur. Habituellement, le client ne le fait qu’une seule fois, via les paramètres du constructeur du directeur. Le réalisateur utilise l'objet constructeur dans toute construction ultérieure. Il existe une approche alternative, où le constructeur passe directement à la méthode de construction du réalisateur.

- Le résultat de la construction ne peut être obtenu directement auprès du directeur que si tous les produits suivent la même interface. Sinon, le client doit récupérer le résultat du générateur.

### Avantages :

- Vous pouvez construire des objets étape par étape, différer les étapes de construction ou exécuter des étapes de manière récursive.
- Vous pouvez réutiliser le même code de construction lors de la création de diverses représentations de produits.
- Principe de responsabilité unique. Vous pouvez isoler le code de construction complexe de la logique métier du produit

### Inconvénients :

- La complexité globale du code augmente car le modèle nécessite la création de plusieurs nouvelles classes.