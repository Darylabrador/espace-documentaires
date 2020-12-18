# Design pattern : Abstract Factory

L' "Abstract Factory" fournit une interface pour créer des familles d'objets liés ou dépendants sans spécifier leurs classes concrètes. 

### Ressources :

- https://refactoring.guru/design-patterns/abstract-factory

### Problématiques :

Imaginez que vous créez un simulateur de magasin de meubles. Votre code se compose de classes qui représentent:

- Une famille de produits connexes, disons: chaise + canapé + table à café.
- Plusieurs variantes de cette famille. Par exemple, les produits Chair + Sofa + CoffeeTable sont disponibles dans les variantes suivantes: Modern, Victorian, ArtDeco.

Vous avez besoin d'un moyen de créer des objets de mobilier individuels afin qu'ils correspondent à d'autres objets de la même famille. Les clients deviennent assez fâchés lorsqu'ils reçoivent des meubles non assortis. De plus, vous ne souhaitez pas modifier le code existant lors de l’ajout de nouveaux produits ou familles de produits au programme. Les vendeurs de meubles mettent à jour leurs catalogues très souvent, et vous ne voudriez pas changer le code de base à chaque fois que cela se produit.

### Solution :

La première chose que suggère le modèle Abstract Factory est de déclarer explicitement les interfaces pour chaque produit distinct de la famille de produits (par exemple, chaise, canapé ou table basse). Ensuite, vous pouvez faire en sorte que toutes les variantes de produits suivent ces interfaces. Par exemple, toutes les variantes de chaise peuvent implémenter l'interface de chaise; toutes les variantes de table basse peuvent implémenter l'interface CoffeeTable, et ainsi de suite.

La prochaine étape consiste à déclarer la fabrique abstraite - une interface avec une liste de méthodes de création pour tous les produits qui font partie de la famille de produits (par exemple, createChair, createSofa et createCoffeeTable). Ces méthodes doivent renvoyer des types de produits abstraits représentés par les interfaces que nous avons extraites précédemment: Chair, Sofa, CoffeeTable, etc.

Pour chaque variante d'une famille de produits, nous créons une classe factory distincte basée sur l'interface AbstractFactory. Une factory est une classe qui renvoie des produits d'un type particulier. Par exemple, ModernFurnitureFactory ne peut créer que des objets ModernChair, ModernSofa et ModernCoffeeTable. Le code client doit fonctionner à la fois avec les factory et les produits via leurs interfaces abstraites respectives. Cela vous permet de modifier le type de fabrique que vous transmettez au code client, ainsi que la variante de produit que le code client reçoit, sans casser le code client réel.

Supposons que le client souhaite qu'une factory produise une chaise. Le client n’a pas besoin de connaître la classe factory, ni le type de chaise qu’il reçoit. Qu'il s'agisse d'un modèle moderne ou d'une chaise de style victorien, le client doit traiter toutes les chaises de la même manière, en utilisant l'interface abstraite Chair. Avec cette approche, la seule chose que le client sait sur la chaise est qu'elle implémente la méthode sitOn() d'une manière ou d'une autre. De plus, quelle que soit la variante de chaise retournée, elle correspondra toujours au type de canapé ou de table basse produit par le même objet factory.

Généralement, l'application crée un objet factory concret au stade de l'initialisation. Juste avant cela, l'application doit sélectionner le type factory en fonction de la configuration ou des paramètres d'environnement.


### Quand est ce qu'il faut l'appliquer ?

- Utilisez l'Abstract Factory lorsque votre code doit fonctionner avec diverses familles de produits associés, mais que vous ne voulez pas qu'il dépende des classes concrètes de ces produits - elles peuvent être inconnues à l'avance ou vous souhaitez simplement permettre une extensibilité future.

### Comment l'implémenter ?

- Cartographiez une matrice de types de produits distincts par rapport aux variantes de ces produits.

- Déclarez des interfaces produit abstraites pour tous les types de produits. Puis faites en sorte que toutes les classes de produits concrètes implémentent ces interfaces.

- Déclarez l'interface de l'usine abstraite avec un ensemble de méthodes de création pour tous les produits abstraits.

- Implémentez un ensemble de classes d'usine concrètes, une pour chaque variante de produit.

- Créez un code d'initialisation d'usine quelque part dans l'application. Il doit instancier l'une des classes d'usine concrètes, en fonction de la configuration de l'application ou de l'environnement actuel. Passez cet objet de fabrique à toutes les classes qui construisent des produits.

- Parcourez le code et trouvez tous les appels directs aux constructeurs de produits. Remplacez-les par des appels à la méthode de création appropriée sur l'objet fabrique.

### Avantages :

- Vous pouvez être sûr que les produits issues d'une factory sont compatibles entre eux.

- Vous évitez les couplages serrés entre les produits en concret et le code client.

- Principe de responsabilité unique. Vous pouvez extraire le code de création de produit en un seul endroit, ce qui facilite la prise en charge du code.

- Principe ouvert / fermé. Vous pouvez introduire de nouvelles variantes de produits sans casser le code client existant.

### Inconvénients :

- Le code peut devenir plus compliqué qu'il ne devrait l'être, car de nombreuses nouvelles interfaces et classes sont introduites avec le modèle.