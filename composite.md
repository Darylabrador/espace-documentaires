# Design pattern : Composite

Composite est un modèle de conception structurelle qui vous permet de composer des objets en arborescence, puis de travailler avec ces structures comme s'il s'agissait d'objets individuels.

### Ressources :

- https://refactoring.guru/design-patterns/composite

### Problématiques :

L'utilisation du modèle composite n'a de sens que lorsque le modèle principal de votre application peut être représenté sous forme d'arborescence.

Par exemple, imaginez que vous avez deux types d'objets: les produits et les boîtes. Une boîte peut contenir plusieurs produits ainsi qu'un certain nombre de boîtes plus petites. Ces petites boîtes peuvent également contenir certains produits ou même des boîtes plus petites, et ainsi de suite.

Supposons que vous décidiez de créer un système de commande utilisant ces classes. Les commandes peuvent contenir des produits simples sans emballage, ainsi que des boîtes remplies de produits ... et d'autres boîtes. Comment déterminez-vous le prix total d'une telle commande?

Vous pouvez essayer l'approche directe: déballer toutes les boîtes, passer en revue tous les produits puis calculer le total. Ce serait faisable dans le monde réel; mais dans un programme, ce n’est pas aussi simple que d’exécuter une boucle. Vous devez connaître à l'avance les classes de produits et de boîtes que vous traversez, le niveau d'imbrication des boîtes et d'autres détails désagréables. Tout cela rend l'approche directe soit trop maladroite, soit même impossible.


### Solution :

Le modèle composite vous suggère de travailler avec des produits et des boîtes via une interface commune qui déclare une méthode de calcul du prix total.

Comment cette méthode fonctionnerait-elle? Pour un produit, il s'agit simplement de renvoyer le prix du produit. Pour une boîte, il passait en revue chaque article contenu dans la boîte, demandait son prix, puis renvoyait un total pour cette boîte. Si l'un de ces articles était une boîte plus petite, cette boîte commencerait également à examiner son contenu et ainsi de suite, jusqu'à ce que les prix de tous les composants internes soient calculés. Une boîte pourrait même ajouter un coût supplémentaire au prix final, comme le coût d'emballage.

Le plus grand avantage de cette approche est que vous n’avez pas besoin de vous soucier des classes concrètes d’objets qui composent l’arbre. Vous n'avez pas besoin de savoir si un objet est un produit simple ou une boîte sophistiquée. Vous pouvez tous les traiter de la même manière via l'interface commune. Lorsque vous appelez une méthode, les objets eux-mêmes transmettent la requête dans l'arborescence.


### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle composite lorsque vous devez implémenter une structure d'objet arborescente.
- Utilisez le modèle lorsque vous souhaitez que le code client traite les éléments simples et complexes de manière uniforme.

### Comment l'implémenter ?

- Assurez-vous que le modèle principal de votre application peut être représenté sous forme d'arborescence. Essayez de le décomposer en éléments simples et en conteneurs. N'oubliez pas que les conteneurs doivent pouvoir contenir à la fois des éléments simples et d'autres conteneurs.

- Déclarez l'interface du composant avec une liste de méthodes qui ont du sens pour les composants simples et complexes.

- Créez une classe feuille pour représenter des éléments simples. Un programme peut avoir plusieurs classes feuilles différentes.

- Créez une classe de conteneur pour représenter des éléments complexes. Dans cette classe, fournissez un champ de tableau pour stocker des références à des sous-éléments. Le tableau doit pouvoir stocker à la fois des feuilles et des conteneurs. Assurez-vous donc qu’il est déclaré avec le type d’interface du composant.

- Lors de l'implémentation des méthodes de l'interface du composant, rappelez-vous qu'un conteneur est censé déléguer l'essentiel du travail à des sous-éléments.

- Enfin, définissez les méthodes d'ajout et de suppression des éléments enfants dans le conteneur.
    Gardez à l'esprit que ces opérations peuvent être déclarées dans l'interface du composant. Cela violerait le principe de séparation des interfaces car les méthodes seront vides dans la classe feuille. Cependant, le client pourra traiter tous les éléments de manière égale, même lors de la composition de l'arbre.

### Avantages :

- Vous pouvez travailler plus facilement avec des arborescences complexes: utilisez le polymorphisme et la récursivité à votre avantage.
- Principe ouvert / fermé. Vous pouvez introduire de nouveaux types d'éléments dans l'application sans casser le code existant, qui fonctionne désormais avec l'arborescence d'objets.

### Inconvénients :

- Il peut être difficile de fournir une interface commune pour les classes dont les fonctionnalités diffèrent trop. Dans certains scénarios, vous devrez sur-généraliser l'interface du composant, ce qui la rendra plus difficile à comprendre.