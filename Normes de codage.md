# Général

- Indentez vos structures de contrôles (``IF``, ``FOR``, ``WHILE``, etc.) avec des tabulations pour mieux s'y retrouver.
- Ajoutez des espaces à côté de vos opérateur. Ne faites pas ``a=1`` mais plutôt ``a = 1``.
- Espacez bien votre code pour le rendre lisible.
- Nommez vos variables avec des noms **cohérents** et **compréhensibles**.
- Commentez vos codes : l'objectif et le détail de ce que fait le code pour que celui puisse être repris et compris rapidement (commentaires au dessus de préférence)

# SQL

- Utilisez des alias pour les tables et les vues dans vos requêtes.
- Ecrivez les *keywords* en MAJUSCULES (SELECT, FROM, WHERE).
- Ecrivez le nom des paramètres, variables, tables, vues, curseur, trigger, etc. en minuscules.
- N'utilisez pas de ponctuation ni d'accentuation.
- Utilisez le ``_`` pour séparez les noms qui comportent plusieurs mots. 
- Pour les jointures, privilégiez ``t1.attribut = t2.attribut`` à ``t1.attribut IN (SELECT attribut FROM t2)``.

# Python

Basez vous sur [ce lien](https://www.python.org/dev/peps/pep-0008/) et [celui-ci](https://gist.github.com/sloria/7001839). Le premier lien correspond aux directives dites *PEP8* qui sont utilisées dans l'industrie. Avec Spyder, vous pouvez activer des *warnings* lorsque votre code viole une directive PEP8. Pour cela allez dans ``Preferences -> Editor -> Code Introspection/Analysis`` et cochez la boîte à côté de ``Style analysis (PEP8)``.

En général, préférez l'utilisation de la programmation fonctionnelle dans vos scripts. Principalement il s'agit d'encapsuler le plus possible votre code dans des fonctions que vous appellerez dans votre script. Cela a deux avantages:

- Le code est réutilisable et on évite les copier/coller (redondances).
- Le déroulement du script est plus lisible.

Ajoutez un commentaire pour expliquer une fonction après l'avoir définie. Soyez clair et écrivez des phrases courtes mais complètes.

Privilégiez l'utilisation de noms de variables parlants qui rendent le code lisible. Une fonction lisible ne devrait même pas avoir besoin de commentaires, sauf au tout début.

# JavaScript

Pour Javascript, vous pouvez déjà vous baser sur tous ce qui a été cité précédemment. 

- Pour les constructeurs, il est de convention de nommer les fonctions constructeurs avec une majuscule. Cela ne change rien, n’importe qu’elle fonction peut devenir un constructeur si elle est instanciée avec le mot clé ``new``, mais cela facilite la lecture du code.
