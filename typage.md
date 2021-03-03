# Sujet de veille

Explorer les typages. Qui sont-ils ? Pourquoi les utiliser ? quel intérêt ?

### Qu'est ce que le typage ?

Le typage définit la nature des valeurs que peut prendre une donnée et les opérateurs qui peuvent lui être appliqués. On peut voir le typage comme étant le type de données tel que le booléan, l'entier ou le string. 

Il existe plusieurs typages :

- typage statique et dynamique (verification du type au moment de la compilation et verification pendant l'exécution) ;
- typage explicite et implicite (Utilisateur qui indique les types utiliser et c'est le compilateur qui détermine les types)
- typage fort et faible (le compilateur assure la détection au plus tôt des erreurs de type)

Il existe plusieurs types de données :

- Types prédéfinis (booléen, entier, réel, string)
- Types paramétrés (ex: déclaration des pointeurs en langage C)
- Types énumérés (liste de valeurs possibles pour une variable)
- Types composés (grouper plusieurs champs de types distincts dans une même variable)
- Types hiérarchiques
- Types opaques ( type incomplètement défini et/ou dont la nature est masquée, on peut juste stocker et transmettre)


### Pourquoi utilise-t-on le typage ?

Le typage permet d'anticipé les erreurs de type. Par exemple, lorsqu'on utilise une variable string et qu'on l'affecte une valeur le format booléen.


### Ressources

- https://developer.mozilla.org/fr/docs/Glossary/Dynamic_typing
- https://fr.wikipedia.org/wiki/Typage_fort
- https://fr.wikipedia.org/wiki/Type_(informatique)