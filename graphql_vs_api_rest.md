# Sujet de veille

GraphQL vs API REST 

## GraphQL

GraphQL est un langage de requêtes et un environnement d'exécution, créé par Facebook en 2012, avant d'être publié comme projet open-source en 2015. Une API GraphQL permet de récupérer des données en fonction de la requête client. En REST, c'est la méthode de requête HTTP (GET, POST,...), l'URL ou encore les paramètres envoyés qui définissent les fonctions métiers à appeler et la nature du retour. GraphQL le fait directement avec la requête envoyée en POST. Comme les requêtes POST ne sont pas mises en cache côté serveur, les requêtes GraphQL doivent être mises en cache côté client4. 

Une API GraphQL est organisée grâce aux Types et Champs. Pour déclarer l'ensemble de ces éléments, le fournisseur de données doit construire le squelette de l'API. C'est ce schéma qu'il partagera à tous les clients qu'il veut, sans que ceux-ci n'aient besoin de savoir comment les données ont été récupérées.

Dans les types on retrouve :

- Query, contient toutes les requêtes de consultation admises par l'API
- Mutation, contenant toutes les règles de mise à jour des données, comme les insertions par exemple

## API REST

L’élément central derrière REST est la ressource. Une API REST comprend un endpoint différent pour chaque ressource, avec des méthodes de requêtage HTTP différentes. Prenons exemple sur l’API d’un blog, avec 2 ressources, l’une pour les auteurs, l’autre pour les articles. L’endpoint pour chaque ressource peut suivre le pattern suivant :

> METHOD /api/:resource:/:id:

Les API REST peuvent devenir très verbeuses, les opérations standard (create, read, update, delete - CRUD) peuvent être intuitivement effectuées pour chaque ressource. Avec REST, pour mettre à jour une ressource, vous utilisez la méthode PATCH au lieu de GET. Pour écrire une ressource, on utilise POST, et la supprimer DELETE.

## Pourquoi utilisé GraphQL ?

GraphQL est un bon choix architectural si l’application et sa structure de donnée font appel à de nombreuses requêtes. Dans notre exemple du blog, si vous souhaitez requêter un article  pour obtenir l’auteur, les tags et les commentaires, il vous faut au minimum 4 requêtes distinctes. Avec GraphQL, cela peut être effectué de façon plus programmatique, et permettre au client de requêter les seules informations souhaitées au final.

GraphQL est également un bon moyen pour minimiser les modifications liées à la montée de version – ce qui arrive quand les ressources et les schémas de données changent dans  une API REST. En interrogeant précisément les bonnes informations, chaque nouvel élément n’interférera pas avec l’implémentation en place. Si votre jeu de données s’agrandit et si vous devez optimiser vos schémas, GraphQL dissimulera cette complexité et permettra au client d’interagir avec les nouvelles données d’une façon plus cohérente.

## Pourquoi utilisé API Rest ?

D’un autre côté, le plus gros avantage de REST sur GraphQL est la facilité avec laquelle les données peuvent être « cachées » et la transparence des actions effectuées sur l’API. En reprenant l’exemple du blog, lorsqu’on interroge l’article x, la requête est cohérente pour tous les clients. Les données ainsi retournées peuvent être placées dans le cache côté serveur pour d’autres requêtes, et réduire ainsi les opérations de la base  pour accélérer les temps de réponse de l’API.

REST est également le bon choix si l’on doit composer avec des données très structurées, là où les actions effectuées sur les API suivent un pattern prévisible – sur un mode CRUD.

REST et GraphQL ont tous deux leurs propres avantages. Mais au-delà de la scalabilité et de la technologie, il convient de prendre en compte le mode de consommation de l’API. Bien comprendre son marché devient alors clé. Une application traditionnelle CRUD sera mieux servie par une API REST, mais si vous développez un outil interne pour des équipes déjà expérimentées sur GraphQL, ce dernier peut être le bon choix pour maintenir la productivité et réduire toute éventuelle friction – l’inverse est vrai pour REST.