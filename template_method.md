# Design pattern : Template method

La méthode de modèle est un modèle de conception comportementale qui définit le squelette d'un algorithme dans la superclasse, mais permet aux sous-classes de remplacer des étapes spécifiques de l'algorithme sans changer sa structure.

### Ressources :

- https://refactoring.guru/design-patterns/template-method

### Problématiques :

Imaginez que vous créez une application d'exploration de données qui analyse les documents d'entreprise. Les utilisateurs alimentent les documents de l'application dans différents formats (PDF, DOC, CSV) et essaient d'extraire des données significatives de ces documents dans un format uniforme.

La première version de l'application ne pouvait fonctionner qu'avec des fichiers DOC. Dans la version suivante, il était capable de prendre en charge les fichiers CSV. Un mois plus tard, vous lui avez «appris» à extraire des données de fichiers PDF.

À un moment donné, vous avez remarqué que les trois classes ont beaucoup de code similaire. Alors que le code pour traiter divers formats de données était entièrement différent dans toutes les classes, le code pour le traitement et l'analyse des données est presque identique. Ne serait-il pas formidable de se débarrasser de la duplication de code en laissant la structure de l’algorithme intacte?

Il y avait un autre problème lié au code client qui utilisait ces classes. Il contenait de nombreuses conditions qui choisissaient un plan d'action approprié en fonction de la classe de l'objet de traitement. Si les trois classes de traitement avaient une interface commune ou une classe de base, vous pourrez éliminer les conditions dans le code client et utiliser le polymorphisme lors de l’appel de méthodes sur un objet de traitement.

### Solution :

Le modèle de méthode de modèle vous suggère de décomposer un algorithme en une série d'étapes, de transformer ces étapes en méthodes et de placer une série d'appels à ces méthodes dans une méthode de modèle unique. Les étapes peuvent être abstraites ou avoir une implémentation par défaut. Pour utiliser l'algorithme, le client est censé fournir sa propre sous-classe, implémenter toutes les étapes abstraites et remplacer certaines des étapes facultatives si nécessaire (mais pas la méthode du modèle elle-même).

Voyons comment cela se déroulera dans notre application d'exploration de données. Nous pouvons créer une classe de base pour les trois algorithmes d'analyse. Cette classe définit une méthode de modèle consistant en une série d'appels à diverses étapes de traitement de documents.

Au début, nous pouvons déclarer toutes les étapes abstraites, obligeant les sous-classes à fournir leurs propres implémentations pour ces méthodes. Dans notre cas, les sous-classes ont déjà toutes les implémentations nécessaires, donc la seule chose que nous pourrions avoir à faire est d'ajuster les signatures des méthodes pour qu'elles correspondent aux méthodes de la superclasse.

Voyons maintenant ce que nous pouvons faire pour éliminer le code en double. Il semble que le code pour ouvrir / fermer des fichiers et extraire / analyser des données est différent pour différents formats de données, il est donc inutile de toucher à ces méthodes. Cependant, la mise en œuvre d'autres étapes, telles que l'analyse des données brutes et la composition de rapports, est très similaire, elle peut donc être extraite dans la classe de base, où les sous-classes peuvent partager ce code.

Comme vous pouvez le voir, nous avons deux types d'étapes:
- les étapes abstraites doivent être implémentées par chaque sous-classe
- les étapes facultatives ont déjà une implémentation par défaut, mais peuvent toujours être remplacées si nécessaire

Il existe un autre type d'étape, appelé hooks. Un crochet est une étape facultative avec un corps vide. Une méthode de modèle fonctionnerait même si un hook n'est pas remplacé. Habituellement, les hooks sont placés avant et après les étapes cruciales des algorithmes, fournissant aux sous-classes des points d'extension supplémentaires pour un algorithme.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle de méthode de modèle lorsque vous souhaitez permettre aux clients d'étendre uniquement des étapes particulières d'un algorithme, mais pas l'ensemble de l'algorithme ou sa structure.

- Utilisez le modèle lorsque vous avez plusieurs classes qui contiennent des algorithmes presque identiques avec quelques différences mineures. Par conséquent, vous devrez peut-être modifier toutes les classes lorsque l'algorithme change.

### Comment l'implémenter ?


- Analysez l'algorithme cible pour voir si vous pouvez le diviser en étapes. Considérez les étapes communes à toutes les sous-classes et celles qui seront toujours uniques.

- Créez la classe de base abstraite et déclarez la méthode modèle et un ensemble de méthodes abstraites représentant les étapes de l'algorithme. Décrivez la structure de l'algorithme dans la méthode de modèle en exécutant les étapes correspondantes. Envisagez de rendre la méthode de modèle définitive pour empêcher les sous-classes de la remplacer.

- Ce n’est pas grave si toutes les étapes finissent par être abstraites. Cependant, certaines étapes peuvent bénéficier d'une implémentation par défaut. Les sous-classes n'ont pas à implémenter ces méthodes.

- Pensez à ajouter des crochets entre les étapes cruciales de l'algorithme.

- Pour chaque variante de l'algorithme, créez une nouvelle sous-classe concrète. Il doit implémenter toutes les étapes abstraites, mais peut également remplacer certaines des étapes facultatives.

### Avantages :

- Vous pouvez autoriser les clients à remplacer uniquement certaines parties d'un algorithme volumineux, ce qui les rend moins affectés par les modifications qui se produisent dans d'autres parties de l'algorithme.
- Vous pouvez extraire le code dupliqué dans une superclasse.

### Inconvénients :

- Certains clients peuvent être limités par le squelette fourni d'un algorithme.
- Vous pouvez violer le principe de substitution de Liskov en supprimant une implémentation d'étape par défaut via une sous-classe.
- Les méthodes de modèle ont tendance à être plus difficiles à maintenir, plus elles comportent d'étapes.