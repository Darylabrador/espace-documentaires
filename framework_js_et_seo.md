# Sujet de veilles

Une market place utilisant un framework front js est elle pertinante dans le cadre du SEO ? Moyen à mettre en oeuvre pour rendre notre app SEO-friendly ?

## Qu'est-ce que le SEO ?

SEO (Search Engine Optimization) signifie en français : « Optimisation pour les moteurs de recherche ».

Ce terme défini l’ensemble des techniques mises en œuvre pour améliorer la position d’un site web sur les pages de résultats des moteurs de recherche (SERP). On l’appelle aussi référencement naturel. L’objectif d’un expert en référencement naturel est d’améliorer la visibilité des sites web qu’il prend en charge en leur faisant gagner des places sur les moteurs de recherche (Google, mais aussi Yahoo !, Bing, etc.). Le but est de faire se rencontrer les internautes intéressés par des produits / services ou du contenu informatif.

On dit qu’un site est bien optimisé ou référencé s’il se trouve dans les premières position d’un moteur de recherche sur les requêtes souhaitées.


## Le problème du SEO en JS

Le problème avec JS c'est que les robots ne peuvent pas faire du crowling pour analyser les informations car les pages sont construites dynamiquement. Généralement, l'aspect SSR permet aux robots d'être plus rapide tandis que les frameworks JS sont basés sur du CSR.

### Pour être plus précis :

Pour le rendu côté serveur (SSR), tout le contenu HTML est présent dans le code source, ce qui signifie que le moteur de recherche peut le demander, le parcourir et l’indexer immédiatement. Il en résulte un temps d’apparition plus rapide et un classement plus rapide dans les résultats de recherche. Tandis que, pour le rendu côté client (CSR), le HTML devant être indexé n’est révélé que lorsque le JS est entièrement rendu côté client. Ainsi, avec le système à deux vagues actuellement utilisé par Google, il peut s’écouler de quelques heures à une semaine avant que le contenu puisse être parcouru, indexé et commencé à être classé dans les résultats de recherche.


## Les solutions

### Pré-rendering  JS :

Il s’agit essentiellement d’écouter et d’envoyer un snapshot HTML pur au robot du moteur de recherche lorsqu’il demande votre page. Ainsi, l’utilisateur peut toujours profiter des vitesses rapides fournies par CSR, tout en fournissant aux moteurs de recherche le contenu HTML nécessaire à l’indexation et au classement de vos pages.

### JavaScript isomorphe :

Recommandée par Google, cette option consiste à ce que le client et les moteurs de recherche reçoivent une page pré-rendue de contenu HTML indexable à la charge initiale (agissant essentiellement comme SSR). Toutes les fonctionnalités de JS sont ensuite superposées afin d’offrir une performance rapide côté client. 

Il fonctionne aussi mieux pour les utilisateurs et les robots des moteurs de recherche. Cependant, la mise en œuvre peut être délicate, et de nombreux développeurs ont du mal à l’accepter. Elle peut également être très coûteuse étant donné les ressources nécessaires à une mise en œuvre réussie. Des recherches approfondies devraient être menées pour déterminer la meilleure façon d’exécuter la SSR avec votre cadre de travail de l’EM

## Ressources :

- https://www.definitions-marketing.com/definition/seo/
- https://theophile-ordinas.fr/javascript-seo-ssr-ou-csr/ 