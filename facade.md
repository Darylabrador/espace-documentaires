# Design pattern : Facade

Façade est un modèle de conception structurelle qui fournit une interface simplifiée à une bibliothèque, un cadre ou tout autre ensemble complexe de classes.

### Ressources :

- https://refactoring.guru/design-patterns/facade

### Problématiques :

Imaginez que vous deviez faire fonctionner votre code avec un large ensemble d'objets appartenant à une bibliothèque ou un framework sophistiqué. Normalement, vous devez initialiser tous ces objets, suivre les dépendances, exécuter les méthodes dans le bon ordre, etc.

En conséquence, la logique métier de vos classes deviendrait étroitement liée aux détails d'implémentation des classes tierces, ce qui rendrait difficile la compréhension et la maintenance.

### Solution :

Une façade est une classe qui fournit une interface simple à un sous-système complexe contenant de nombreuses pièces mobiles. Une façade peut fournir des fonctionnalités limitées par rapport au travail direct avec le sous-système. Cependant, il n'inclut que les fonctionnalités qui intéressent vraiment les clients.

Avoir une façade est pratique lorsque vous avez besoin d'intégrer votre application à une bibliothèque sophistiquée qui possède des dizaines de fonctionnalités, mais vous avez juste besoin d'un tout petit peu de ses fonctionnalités.

Par exemple, une application qui télécharge de courtes vidéos amusantes avec des chats sur les médias sociaux pourrait potentiellement utiliser une bibliothèque de conversion vidéo professionnelle. Cependant, tout ce dont il a vraiment besoin est une classe avec la méthode unique encoder (nom de fichier, format). Après avoir créé un tel cours et l'avoir connecté à la bibliothèque de conversion vidéo, vous aurez votre première façade.

### Quand est ce qu'il faut l'appliquer ?

- Utilisez le modèle de façade lorsque vous avez besoin d'une interface limitée mais simple avec un sous-système complexe.
- Utilisez la façade lorsque vous souhaitez structurer un sous-système en couches.

### Comment l'implémenter ?

- Vérifiez s'il est possible de fournir une interface plus simple que ce que propose déjà un sous-système existant. Vous êtes sur la bonne voie si cette interface rend le code client indépendant de la plupart des classes du sous-système.

- Déclarez et implémentez cette interface dans une nouvelle classe de façade. La façade doit rediriger les appels du code client vers les objets appropriés du sous-système. La façade doit être responsable de l'initialisation du sous-système et de la gestion de son cycle de vie ultérieur à moins que le code client ne le fasse déjà.

- Pour profiter pleinement du pattern, faites communiquer tout le code client avec le sous-système uniquement via la façade. Désormais, le code client est protégé de toute modification du code du sous-système. Par exemple, lorsqu'un sous-système est mis à niveau vers une nouvelle version, il vous suffira de modifier le code de la façade.

- Si la façade devient trop grande, envisagez d'extraire une partie de son comportement dans une nouvelle classe de façade raffinée.

### Avantages :

- Vous pouvez isoler votre code de la complexité d'un sous-système.

### Inconvénients :

- Une façade peut devenir un objet divin couplé à toutes les classes d'une application.