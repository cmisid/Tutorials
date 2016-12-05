# Développement React

## Résumé

React est un *framework* pour développer des interfaces utilisateurs. Comme ses concurrents (notamment Vue.js et Angular), React marque un changement brutal dans la façon de concevoir une interface utilisateur.

Avant, on écrivait des directives pour mettre à jour l'interface; on disait de façon impérative à l'application de faire telle action. Avec React on va plutôt lier des données à l'interface. Lorsque les données sont mises à jour, alors l'interface se mettra à jour elle même; React s'en chargera, le développeur n'a pas besoin d'y réfléchir. React est donc un langage déclaratif où l'on code deux types de choses:

- Des déclarations de composants où l'on précise les liaisons données/programmes.
- Des fonctions pour mettre à jour les données.

Et c'est tout. React encourage fortement à réfléchir à une interface en termes de *composants*. Un composant est simplement un morceau de l'interface (une liste, un bouton, etc.) Des composants peuvent appartenir à d'autres composants, on parle alors d'affiliation parent/enfant ("parent/child" en anglais). La communication entre un parent et un enfant se fait dans le sens "parent vers enfant". Concrètement un parent fait passer des *props* (qui sont des données) à ses enfants pour que ceux-ci puisse les afficher.

Il faut bien prendre en compte le fait que développer veut dire qu'on doit se familiariser avec d'autres concepts faisant partis de l'écosystème JavaScript moderne. Le reste de ce document regroupe des liens vers différentes explications permettant de se familiariser avec cet écosytème dont React fait parti.

## React

- [Tutoriel officiel par Facebook](https://facebook.github.io/react/tutorial/tutorial.html)
- [Tutoriel vidéo par Egghead](https://egghead.io/courses/react-fundamentals)

## React Native

React est devenu tellement populaire qu'une variante pour mobile a vu le jour: React Native. Cette variante possède la même syntaxe que React (c'est le même moteur derrière). React Native permet de développer une application en JavaScript qui va ensuite se *transpiler* en Objective-C (pour iOS) et en Java (pour Android). De cette façon on peut développer une application mobile qui marche sur les deux plateformes! Tout ce qui s'applique à React s'applique à React Native (quasiment).

- [Tutoriel officiel par Facebook](https://facebook.github.io/react-native/docs/getting-started.html#content)
- [Tutoriel vidéo par Egghead](https://egghead.io/courses/react-native-fundamentals)
- [Mise en page avec le système Flexbox](http://moduscreate.com/react-native-layout-system/)
- [Exemple de développement du début à la fin](https://www.raywenderlich.com/126063/react-native-tutorial)

## ES6

L'ES6 est une syntaxe particulière du JavaScript qui date de 2015. C'est une syntaxe qui permet de coder de façon plus fonctionnelle et moins impérative. C'est une syntaxe puissante qui est recommandé pour le développement React. D'ailleurs elle est fourni de base lorsque l'on créé une application React ou React Native en suivant la documentation officielle. A l'heure actuelle un code écrit en ES6 se fait compiler en JavaScript "classique" avec un outil qui s'appelle Babel.

- [Slides d'introduction en français](http://fr.slideshare.net/jucrouzet/prsentation-de-ecmascript-6)
- [Tutoriel vidéo par Egghead](https://egghead.io/courses/learn-es6-ecmascript-2015)
- [Documentation sur Lodash](https://lodash.com/docs/4.17.2), une librairie incontournable pour manipuler des données en JavaScript. Plus besoin de coder des choses de tous les jours à l'arrache!
