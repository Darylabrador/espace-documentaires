## Behavioral design patterns

Ces modèles de conception concernent tous la communication des objets de Class. Les modèles comportementaux sont les modèles les plus spécifiquement concernés par la communication entre les objets.

Autrement dit, ils concernent les algorithmes et l'attribution des responsabilités entre les objets.

### Ressources :

- https://refactoring.guru/design-patterns/behavioral-patterns
- https://sourcemaking.com/design_patterns 


### Chain of Responsibility

La chaîne de responsabilité est un modèle de conception comportementale qui vous permet de transmettre des demandes le long d'une chaîne de gestionnaires. À la réception d'une demande, chaque gestionnaire décide soit de traiter la demande, soit de la transmettre au gestionnaire suivant de la chaîne.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/command"> https://refactoring.guru/design-patterns/command </a>


### Command

La commande est un modèle de conception comportementale qui transforme une demande en un objet autonome contenant toutes les informations sur la demande. Cette transformation vous permet de paramétrer des méthodes avec différentes requêtes, de retarder ou de mettre en file d'attente l'exécution d'une requête et de prendre en charge les opérations annulables.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/command"> https://refactoring.guru/design-patterns/command </a>


### Iterator

Iterator est un modèle de conception comportementale qui vous permet de parcourir les éléments d'une collection sans exposer sa représentation sous-jacente (liste, pile, arbre, etc.).

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/iterator"> https://refactoring.guru/design-patterns/iterator </a>


### Mediator

Mediator est un modèle de conception comportementale qui vous permet de réduire les dépendances chaotiques entre les objets. Le modèle restreint les communications directes entre les objets et les oblige à collaborer uniquement via un objet médiateur.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/mediator"> https://refactoring.guru/design-patterns/mediator </a>


### Memento

Memento est un modèle de conception comportementale qui vous permet d'enregistrer et de restaurer l'état précédent d'un objet sans révéler les détails de son implémentation.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/memento"> https://refactoring.guru/design-patterns/memento </a>


### Observer

Observer est un modèle de conception comportementale qui vous permet de définir un mécanisme d’abonnement pour informer plusieurs objets de tout événement survenant à l’objet qu’ils observent.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/observer"> https://refactoring.guru/design-patterns/observer </a>


### State

L'état est un modèle de conception comportementale qui permet à un objet de modifier son comportement lorsque son état interne change. Il semble que l'objet ait changé de classe.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/state"> https://refactoring.guru/design-patterns/state </a>


### Strategy

La stratégie est un modèle de conception comportementale qui vous permet de définir une famille d'algorithmes, de placer chacun d'eux dans une classe distincte et de rendre leurs objets interchangeables.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/strategy"> https://refactoring.guru/design-patterns/strategy </a>


### Template Method

La méthode de modèle est un modèle de conception comportementale qui définit le squelette d'un algorithme dans la superclasse, mais permet aux sous-classes de remplacer des étapes spécifiques de l'algorithme sans changer sa structure.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/template-method"> https://refactoring.guru/design-patterns/template-method </a>


### Visitor

Visitor est un modèle de conception comportementale qui vous permet de séparer les algorithmes des objets sur lesquels ils opèrent.

Plus de détails sur  : <a href="https://refactoring.guru/design-patterns/visitor"> https://refactoring.guru/design-patterns/visitor </a>