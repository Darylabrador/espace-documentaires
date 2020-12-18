# Design pattern : Singleton

Il s'agit ici d'un modèle de conception créative qui permet de nous assurer qu'une classe n'a qu'une seule instance, tout en fournissant un point d'accès globale à cette instance.

### Ressources pour aller plus loin :

- https://refactoring.guru/design-patterns/singleton

### Problématiques :

Le modèle Singleton résout deux problèmes en même temps, violant le principe de responsabilité unique :

- Assurez-vous qu'une classe n'a qu'une seule instance.
- Fournissez un point d'accès global à cette instance.

De nos jours, le modèle Singleton est devenu si populaire que les gens peuvent appeler quelque chose un singleton même s'il ne résout qu'un des problèmes énumérés.

### Solution :

Toutes les implémentations du Singleton ont ces deux étapes en commun :

- Rendez le constructeur par défaut privé, pour empêcher d'autres objets d'utiliser l'opérateur new avec la classe Singleton.

- Créez une méthode de création statique qui agit comme un constructeur. Sous le capot, cette méthode appelle le constructeur privé pour créer un objet et l'enregistre dans un champ statique. Tous les appels suivants à cette méthode renvoient l'objet mis en cache.

- Si votre code a accès à la classe Singleton, il peut appeler la méthode statique de Singleton. Ainsi, chaque fois que cette méthode est appelée, le même objet est toujours renvoyé.

Exemple :

Le gouvernement est un excellent exemple du modèle Singleton. Un pays ne peut avoir qu'un seul gouvernement officiel. Indépendamment de l'identité personnelle des individus qui forment les gouvernements, le titre «Le gouvernement de X» est un point d'accès mondial qui identifie le groupe de personnes en charge

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle Singleton lorsqu'une classe de votre programme ne doit avoir qu'une seule instance disponible pour tous les clients; par exemple, un seul objet de base de données partagé par différentes parties du programme.

- Utilisez le modèle Singleton lorsque vous avez besoin d'un contrôle plus strict sur les variables globales.

### Comment l'implémenter ?

- Ajoutez un champ statique privé à la classe pour stocker l'instance de singleton.

- Déclarez une méthode de création statique publique pour obtenir l'instance singleton.

- Implémentez «l'initialisation paresseuse» dans la méthode statique. Il doit créer un nouvel objet lors de son premier appel et le placer dans le champ statique. La méthode doit toujours renvoyer cette instance sur tous les appels suivants.

- Rendez le constructeur de la classe privé. La méthode statique de la classe pourra toujours appeler le constructeur, mais pas les autres objets.

- Passez en revue le code client et remplacez tous les appels directs au constructeur du singleton par des appels à sa méthode de création statique.

### Avantages :

- Vous pouvez être sûr qu'une classe n'a qu'une seule instance.
- Vous obtenez un point d'accès global à cette instance.
- L’objet singleton n’est initialisé que lorsqu’il est demandé pour la première fois.

### Inconvénients :

- Viole le principe de responsabilité unique. Le modèle résout deux problèmes à la fois.

- Le modèle Singleton peut masquer une mauvaise conception, par exemple, lorsque les composants du programme en savent trop les uns sur les autres.

- Le modèle nécessite un traitement spécial dans un environnement multithread afin que plusieurs threads ne créent pas plusieurs fois un objet singleton.

- Le test unitaire du code client du Singleton peut être difficile car de nombreux frameworks de test reposent sur l'héritage lors de la production d'objets fictifs. Étant donné que le constructeur de la classe singleton est privé et que la substitution des méthodes statiques est impossible dans la plupart des langages, vous devrez penser à une manière créative de se moquer du singleton. Ou n’écrivez pas les tests. Ou n’utilisez pas le modèle Singleton.