<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table des matières** 

- [Avant-propos](#avant-propos)
- [Architecture](#architecture)
  - [Objectif](#objectif)
  - [Structure concrète](#structure-concr%C3%A8te)
    - [L'application](#lapplication)
    - [Le code](#le-code)
    - [Les fonctions](#les-fonctions)
- [Documentation](#documentation)
- [Tests](#tests)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Avant-propos

En plus de coder, un développeur doit aussi penser à ce qui entoure le code. Ces tâches peuvent paraître anodines et sont souvent délaissées par les développeurs. La plupart du temps ce sont des tâches qui sont considérées comme des pertes de temps.

Au contraire, il faut bien comprendre que le temps que l'on prend pour structurer, documenter et élaborer des tests fait gagner tellement de temps sur le long terme.

- Il faut structurer pour rendre une application modulable et cohérente.
- Il faut documenter pour faire comprendre l'application aux nouveaux développeurs.
- Il faut tester pour que l'application fonctionne comme voulu en production.

Un projet est un édifice qui doit fonctionner pendant des années. Son code sera ré-utilisé. On y ajoutera des fonctionnalités. On lui demandera de faire tout et n'importe quoi. **Il faut commencer sur de bonnes bases si on veut construire quelque chose qui doit durer**.  

# Architecture

## Objectif

La tendance moderne (et celle que nous utiliserons) est l'**architecture en microservices**. L'idée est de séparer, à plusieurs niveaux, un projet en plusieurs **services** (autrement dit des sous-projets). C'est déjà ce qu'on fait en répartissant le travail sur 10 groupes.

Ce qui nous intéresse est la division à plus basse échelle, au sein d'un sous-projet. Il faut commencer par scinder le sous-projet en **tâches** indépendantes. Les tâches sont reliées pas une **interface**. L'objectif est que si on modifie la façon dont on résout une tâche, il ne faille pas modifier les autres tâches qui en dépendent. Au contraire il faudra seulement changer l'interface entre les tâches, ou bien faire en sorte que la tâche modifiée génère la même interface qu'avant.

Voici un exemple d'architecture en microservices:

![Architecture en microservices](http://i.imgur.com/f8b9TKc.png)

Les rectangles représentent un morceau de code qui fait quelque chose de spécifique et de confiné. Les nuages représentent la façon dont les morceaux de codes communiquent entre eux. Il faut donc raisonner en termes d'**entrées** et de **sorties**. Si jamais on veut changer un morceau de l'application, le reste de l'application doit toujours fonctionner.

## Structure concrète

### L'application

Au niveau de l'application, le minimum requis est le suivant:

- Un dossier ``lib/`` qui contient tout le code de l'application.
- Un dossier ``setup/`` qui regroupe les scripts d'installation de l'application.
- Un dossier ``tests/`` qui contient tous les tests relatifs à l'application.

### Le code

Le code doit être séparée en dossiers. Par exemple, un dossier contient tout le code nécessaire pour communiquer avec la base de données, alors qu'un autre regroupe le code relatif au calcul des distances.

### Les fonctions

A un niveau plus fin, les morceaux de code doivent être structurés en fonctions avec une définition claire des entrées et des sorties de chaque fonction.

# Documentation

Le plus important est que la documentation découle de la structure. Chaque dossier (un morceau de l'application) doit contenir un document, le *README*, qui explicite clairement les choix qui ont été fait lors de l'élaboration et du codage du morceau de l'application.

La rédaction des README doit indiquer tout ce qu'un nouveau développeur devrait savoir. Le style doit être clair et précis. Faites des phrases courtes avec des verbes. Structurez le README logiquement, par exemple avec une section par script et une sous-catégorie par fonction. Mettez vous toujours à la place de quelqu'un qui découvre et ne soyez pas fainéants dans vos propos.

Il n'y a pas beaucoup de monde qui aime faire de la documentation, c'est normal. Et pourtant c'est souvent pour la documentation qu'un projet devient populaire. Cela ne sert absolument à rien de coder un bloc illisible, qui fonctionne jusqu'à ce quelqu'un souhaite ajouter une fonctionnalité et perde des heures à déchiffrer le code.

# Tests

Lorsqu'on ajoute une fonctionnalité à une application, on va naturellement lancer l'application pour vérifier que tout fonctionne. Evidemment c'est un processus très répétitif et qui ouvre la voie à l'erreur humaine. Les tests sont là pour s'assurer que les contraintes que l'on a imposé sont respectées.

De la même façon que pour la documentation, les tests sont souvent délaissés par les développeurs. Et pourtant ces mêmes développeurs passent souvent un temps non négligeable à chercher les erreurs dans leur code. Une bonne pratique est de définir les tests avant le codage afin d'être certain que la sortie code soit ce que l'on attend, c'est ce qu'on appelle le [test driven development](https://www.google.fr/webhp?sourceid=chrome-instant&ion=1&espv=2&es_th=1&ie=UTF-8#q=test%20driven%20development&es_th=1). Il faut comprendre que les tests permettent de confirmer que tout ce que l'on a fait avant fonctionne parfaitement. **Le test en algorithmique est l'équivalent de la démonstration en mathématique**.

Des exemples de tests sont:

- S'assurer qu'une fonction réponde en moins d'une seconde au moins 90% du temps.
- L'indentation du code n'est pas trop profonde (complexité abusive), maximum 3.
- Faire de la [couverture de code](https://www.wikiwand.com/fr/Couverture_de_code).
- S'assurer que la fonction gère tous les cas possibles de paramètre d'entrée.
- Vérifier que le ratio commentaires/code soit supérieur à un seuil fixé.
- Faire de la [métrique de code](https://www.wikiwand.com/fr/M%C3%A9trique_(logiciel)).
- Faire de la [revue de code](https://www.wikiwand.com/fr/Revue_de_code).
- Faire des [tests unitaires](https://www.wikiwand.com/fr/Test_unitaire). Par exemple s'assurer que la sortie d'une fonction corresponde à ce qu'on s'attendait au vu des paramètres d'entrée.
- Faire de la [traçabilité des exigences](https://www.wikiwand.com/fr/Gestion_des_exigences#/Tra.C3.A7abilit.C3.A9_des_exigences).


Chaque langage possède sa propre syntaxe de tests. Pour ce qui est de Python, vous pouvez vous référer [ici](https://github.com/TaxiSID/Documentation/wiki/Introduction-au-langage-Python#faire-des-tests). En général réfléchissez toujours à tous les cas auxquels vos fonctions vont faire face, prenez le temps et soyez assidus.

Les tests ne sont pas à négliger. Le logiciel [SQLite](https://www.sqlite.org/src/doc/trunk/README.md) est un exemple parfait de ce vers quoi devraient tendre tous les logiciels. SQLite comporte tellement de tests qui le rendent sans faille qu'Apple et Google l'ont adopté pour leur systèmes d'exploitation mobiles car ils savent que SQLite ne peut raisonnablement pas planter.