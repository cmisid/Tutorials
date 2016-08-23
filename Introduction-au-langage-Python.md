# Avant-propos

Durant le projet nous utiliserons en grande partie le langage Python. Bien qu'il ne soit pas enseigné en SID, ce n'est pas un langage complexe. Au contraire, la syntaxe est plus claire que d'autres langages et on s'y habitue très vite par rapport à d'autres langages.

Les avantages de Python sont nombreux. D'une part c'est sans doute le langage de script le plus utilisé au monde car on peut quasiment tout faire avec: programmation web, statistiques, machine learning, gestion de bases de données... La communauté de Python est la plus grande dans le monde de la programmation: si vous voulez quelque chose, quelqu'un l'a sûrement déjà fait. Quelque soit votre problème en Python vous pourrez trouver la solution sur le net sans trop de problème, même en français.

Nous utiliserons donc Python pour générer des pages web et pour gérer une base de données. Il y a évidemment beaucoup d'avantages à ce que tous les groupes utilisent le même langage de programmation. Les élèves pourront s'entraider et la distribution du code se fera plus aisément, surtout en combinaison avec GitHub.

Enfin, il faut dire que ça vaut la peine de s'intéresser à Python, c'est un langage qui sera forcément présent dans l'écosystème informatique des années à venir.

# Table des matières
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
- [Installation](#installation)
- [Syntaxe générale](#syntaxe-g%C3%A9n%C3%A9rale)
  - [Variables et assignement](#variables-et-assignement)
  - [Syntaxe](#syntaxe)
  - [Structures de contrôle](#structures-de-contr%C3%B4le)
    - [`if... else`](#if-else)
    - [Boucle `for... in`](#boucle-for-in)
      - [La fonction `range`](#la-fonction-range)
    - [Boucle `while`](#boucle-while)
    - [Interrompre les boucles: `break`, `continue` et `return`](#interrompre-les-boucles-break-continue-et-return)
  - [Listes](#listes)
    - [Compréhensions](#compr%C3%A9hensions)
    - [Opérateurs fonctionnels sur les listes](#op%C3%A9rateurs-fonctionnels-sur-les-listes)
  - [Fonctions](#fonctions)
  - [Crédits](#cr%C3%A9dits)
- [Installation de librairies](#installation-de-librairies)
- [Programmation web](#programmation-web)
  - [Les templates](#les-templates)
- [Exemple de template avec Flask](#exemple-de-template-avec-flask)
  - [Les vues](#les-vues)
  - [Structure du projet](#structure-du-projet)
  - [Conclusion](#conclusion)
- [Gestion d'une base de données](#gestion-dune-base-de-donn%C3%A9es)
  - [Création de la base de données](#cr%C3%A9ation-de-la-base-de-donn%C3%A9es)
  - [Définir une connexion](#d%C3%A9finir-une-connexion)
  - [Créer des tables](#cr%C3%A9er-des-tables)
  - [Peupler les tables](#peupler-les-tables)
  - [Faire des requêtes sur les tables](#faire-des-requ%C3%AAtes-sur-les-tables)
  - [Conclusion](#conclusion-1)
- [Faire des tests](#faire-des-tests)
- [Liens](#liens)
  - [Le langage Python](#le-langage-python)
  - [Flask](#flask)
  - [PostgreSQL](#postgresql)
- [Conclusion](#conclusion-2)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Installation

Il y'a deux versions de Python, la 2 et la 3. La 2 ne sera plus maintenue à partir de 2017, il vaut donc mieux se mettre directement à la 3 (on est actuellement à la version 3.5). La raison pour laquelle certaines personnes ne veulent pas passer de la 2 à la 3 est que certaines librairies existent seulement pour la version 2, mais c'est de plus en plus négligeable.

Il existe de nombreuses façons d'installer Python, une des meilleures est d'utiliser le package Anaconda. En plus d'installer Python, Anaconda contient des librairies célèbres comme ``numpy``, ``scipy`` et ``pandas`` (nous en parlerons plus tard) et une interface graphique très pratique qui s'appelle Spyder (un peu comme RStudio pour le langage R).

- Commencer par télécharger la version 3.5 d'Anaconda [ici](https://www.continuum.io/downloads).
- Pour Mac et Windows, vous aurez maintenant accès à une application qui s'appelle ``Anaconda``, quand vous l'ouvrez vous devriez obtenir le menu suivant:

![Anaconda](http://i.imgur.com/eZ5pQ1j.png)

- Sur Ubuntu, il vous faudra lacer les commandes suivantes:

```sh
# On accède au dossier ``téléchargements``
cd téléchargements/
# On autorise le script à s'exécuter 
chmod +x Anaconda3-2.4.1-Linux-x86_64.sh
# On l'exécute
./Anaconda3-2.4.1-Linux-x86_64.sh
# On dit au système qu'il doit utiliser le Python d'Anaconda
export PATH="$HOME/anaconda/bin:$PATH"
```

- Lancez maintenant l'application Spyder à partir du menu (le chargement prend un peu de temps). L'interface ressemble à l'image suivante:

![Spyder](http://i.imgur.com/E8NnJA2.png)

- Voilà, vous avez installé Python et vous pouvez commencer à coder!

Spyder se découpe en trois parties. A gauche vous pouvez écrire vos scripts (des fichiers qui se terminent en ``.py``). Vous pouvez l'exécutez avec le raccourci ``Commande+Entrée`` ou bien en cliquant sur la flèche verte dans la barre d'outils. Le code s'exécute dans le terminal en bas à droite. Enfin, on peut voir les variables que l'on manipule de façon élégante dans la fenêtre en haut à droite.

Le terminal d'en bas à droite est en fait un "super-terminal" destiné spécifiquement au développement Python, il s'appelle IPython et regorge de nombreuses fonctionnalités très pratiques. Par exemple, sur l'image précédente, le graphique s'affiche dans le terminal, cela et d'autres petites choses sont évidemment des artifices, mais elles rendent la développement bien plus agréable.

# Syntaxe générale

## Variables et assignement

Python est un langage dynamiquement typé, les variables n'ont pas
besoin d'être déclarées, et leur type peut changer au cours de
l'exécution.

``` python
python: a = 3
python: type(a)
<type 'int'>
python: a = '3'
python: type(a)
<type 'str'>
python: a
'3'
python: int(a)
3
``` 

## Syntaxe

L'indentation en Python a une valeur syntaxique : elle sert à délimter
les blocs. Toutes les lignes d'un même bloc doivent être précédées du
même nombre d'espaces blancs ; en général on conseille d'utiliser 4
espaces blancs.

Voici un exemple de bloc conditionnel mettant en évidence cette
syntaxe.

``` python
if a == 0:
    print 'a vaut 0'
elif a > 0:
    print('a est positif')
    print('il vaut : ', a)
else:
    print('a est négatif')
print 'encore des questions sur a?'
```

Les retours à la ligne sont interdits en Python, sauf entre
parenthèses `()`, crochets `[]`, et accolades `{}`. L'exemple suivant
est incorrect :

``` python
if a == b
   and c == d:
    print('yes')
```

Alors que ceci est correct (et équivalent à la sémantique entendue):

``` python
if (a == b
    and c == d):
    print('yes')
```


## Structures de contrôle

Source : <https://docs.python.org/3.5/tutorial/controlflow.html>

### `if... else`

La seule construction conditionnelle existante en Python est
`if... elif... else...`. Toutes les branches sont optionnelles, à
l'exception du `if`, il peut y avoir un nombre quelconque de `elif`,
mais un seul `else` à la fin.

``` python
if a == b == c:
    print('égaux')
elif a <= b <= c  or  c <= b <= a:
    print 'b au milieu'
elif b <= a <= c  or  c <= a <= b:
    print('a au milieu')
else:
    print('c au milieu')
``` 

### Boucle `for... in`

Il existe deux types de boucles en Python. La plus couramment utilisée
est le `for... in` qui permet de parcourir les éléments d'une liste.

``` python
for i in range(10):
    print(i)
``` 

#### La fonction `range`

La boucle `for` est souvent utilisée en conjonction avec la fonction
`range`, dont la syntaxe générale est :

``` python
range(start, end, step)
``` 

Ainsi appelée, la fonction génère la liste des entiers entre `start`
(inclus) et `end` (non inclus) avec pas de `step` :

``` python
python: range(0, 10, 2)
[0, 2, 4, 6, 8]
``` 

Les deux autres syntaxes admissibles sont `range(start, end)` (pas
égal à 1) et `range(end)` (début égal à 0).

**Note :** À partir de Python 3.x, `range` ne renvoie plus une liste,
 mais un *générateur*. La différence réside exclusivement dans
 l'utilisation de la mémoire, beaucoup plus efficace avec la 3.x. Le
 même comportement est réalisé par la fonction `xrange` en Python 2.x.

### Boucle `while`

La deuxième boucle est très similaire à la boucle `while` en C.

``` python
a = 0
while a < 10:
    a += 1
    print(a)
``` 

Pas étonnant qu'il soit alors beaucoup plus facile d'écrire une boucle
infinie :

``` python
while True:
    print('boucle toujours')
``` 

### Interrompre les boucles: `break`, `continue` et `return`

Comme en C, l'instruction `break` sort de la boucle sans vérifier la
condition :

``` python
for i in range(10):
    print(i)
    if i > 2:
        break
``` 

L'instruction `continue` passe à l'itération suivante en sautant le
reste du corps :

``` python
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
``` 

Et le `return` sort immédiatement de toute boucle et de la fonction
qui le contient.


## Listes

Source : <https://docs.python.org/3.5/tutorial/datastructures.html#more-on-lists>

L'un des objets les plus utilisés en Python, ce sont les listes. On
déclare une liste avec les crochets `[]`, et on accède à ses éléments
comme on accède aux éléments d'un tableau en C :

``` python
python: l = [1, 2, 'a', True]
python: l
[1, 2, 'a', True]
python: l[0]
1
python: l[3]
True
python: l[4]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
``` 

La syntaxe pour accéder aux éléments d'une liste est plus puissante en
Python qu'en C. Les indices négatifs accèdent aux éléments à partir du
dernier :

``` python
python: l[-1]
True
python: l[-4]
1
python: l[-5]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
``` 

Il est aussi possible d'obtenir les sous-listes d'une liste avec une
syntaxe qui rappelle les paramètres de la fonction
`range`. L'expression `l[start:end:step]` donne la sous-liste de `l`
qui démarre à l'élément `start` (inclus), se termine à l'élément `end`
(exclus) et saute tous les `step` éléments. Chacun des composants peut
être omis, il prendra alors une valeur par défaut (0 pour `start`, la
longueur de la liste pour `end`, 1 pour `step`).

``` python
python: l = range(10)
python: l
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
python: l[0:4]
[0, 1, 2, 3]
python: l[0:4:2]
[0, 2]
python: l[2:]
[2, 3, 4, 5, 6, 7, 8, 9]
python: l[:-3]
[0, 1, 2, 3, 4, 5, 6]
python: l[0::3]
[0, 3, 6, 9]
python: l[4:-2]
[4, 5, 6, 7]
python: l[::]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
python: l[:]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

``` 

La syntaxe `[:]` est un raccourci courant pour *copier* une liste :

``` python
python: l[:] == l
True
python: l[:] is l
False
``` 

### Compréhensions

Python offre une syntaxe pour la création des listes qui devrait être
familière aux mathématiciens. C'est un héritage du langage Lisp appelé
*compréhensions de listes* :

``` python
python: [a + 0.5 for a in range(10)]
[0.5, 1.5, 2.5, 3.5, 4.5, 5.5, 6.5, 7.5, 8.5, 9.5]
``` 

ce qui est sémantiquement équivalent à

``` python
l = []
for a in range(10):
    l.append(a + 0.5)
``` 

On peut ajouter un nombre arbitraire de `for` et de `if` (sans `else`)
dans une compréhension, ils seront déroulés dans l'ordre :

``` python
[x*y for x in range(10)
     for y in range(x)
     if (x + y) % 2 == 0]
``` 

(les retours à la ligne sont optionnels) est équivalent à

``` python
l = []
for x in range(10):
    for y in range(x):
        if (x + y) % 2 == 0:
            l.append(x*y)
``` 

### Opérateurs fonctionnels sur les listes

Python définit quelques fonctions typiques des langages fonctionnels
pour traiter efficacement une liste. Les plus importantes sont `map`,
`filter`, et `reduce` ; elles laissent inchangée la liste d'origine.

`map` applique une fonction à chaque élément d'une liste et renvoie la
liste des résultats. Dans l'exemple ci-dessous, `hex` est la fonction
qui renvoie la représentation hexadécimale d'un entier :

``` python
python: map(hex, range(10,20))
['0xa', '0xb', '0xc', '0xd', '0xe', '0xf', '0x10', '0x11', '0x12', '0x13']
``` 

`filter` applique une fonction à chaque élément d'une liste et renvoie
la liste des éléments pour lesquels la fonction à donné
`True`. L'exemple suivant utilise la fonction `is_prime` de Sage, qui
teste la primalité de son paramètre :

``` python
sage: filter(is_prime, range(20))
[2, 3, 5, 7, 11, 13, 17, 19]
``` 

`reduce` parcourt la liste de gauche à droite. Le résultat de chaque
itération est obtenu en appliquant une fonction bivariée au résultat
de l'itération précédente et à l'élément courant. Dans l'exemple
suivant, `reduce` calcule la somme des entiers de 0 à 9 ; la fonction
standard `operator.add` est l'équivalent de l'opérateur `+` :

``` python
python: import operator
python: reduce(operator.add, range(10))
45
``` 

À partir de l'opérateur `reduce`, il est facile de définir quelques
autres fonctions très utiles : `sum`, `all`, `any`, `max`, `min`,
`join`. Vous êtes invités à en lire la documentation.



## Fonctions

Source : <https://docs.python.org/3.5/tutorial/controlflow.html>

Les fonctions Python sont définies par le mot clef `def`. Elles
peuvent prendre un nombre arbitraire de paramètres, et renvoyent une
valeur à l'aide du mot clef `return`. Toute fonction renvoye une
valeur, les fonctions qui n'ont pas de `return` renvoient la valeur
spéciale `None`.

``` python
def max(x, y):
    if x > y:
        return x
    else:
        return y
``` 

Certains paramètres peuvent prendre des valeurs par défaut. Si un
paramètre prend une valeur par défaut, tous ceux qui le suivent
doivent aussi en prendre.

``` python
python: def test(a, b, c=0, d=False):
.......    return a, b, c, d

python: test(1, 2)
(1, 2, 0, False)
python: test(1, 2, 3)
(1, 2, 3, False)
python: test(1, 2, 3, 4)
(1, 2, 3, 4)
python: test(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: test() takes at least 2 arguments (1 given)
``` 

Les paramètres d'une fonction peuvent être assignés hors ordre avec la
notation `paramètre=valeur` :

``` python
python: test(b=1, a=2)
(2, 1, 0, False)
python: test(1, 2, d=4)
(1, 2, 0, 4)
``` 

Python fournit deux opérateurs unaires pour transformer des objets en
paramètres d'une fonction. L'opérateur `*` transforme une liste ou un
tuple, tandis que l'opérateur `**` transforme un dictionnaire :

``` python
python: l = range(4)
python: test(*a)
(0, 1, 2, 3)
python: d = { 'a' : 3, 'b' : 5, 'd' : 1 }
python: test(**d)
(3, 5, 0, 1)
``` 

## Crédits
Original : [Luca de Feo](https://github.com/defeo/MA2-ace) - *GitHub*  
Modifications (cohérence Python 3.x) : [Axel Bellec](https://github.com/belekkk) - *GitHub*  


# Installation de librairies

L'installation de nouvelles librairies se fait au travers de la commande ``pip``. Comme nous utilisons Anaconda, toutes nos librairies seront contenus dans le dossier ``anaconda`` qui se trouve maintenant dans vos documents. On peut donc installer la librairie ``numpy`` en faisant

```sh
anaconda/bin/pip install numpy
```

Cependant, on peut très bien faire cela grâce au terminal IPython de Spyder, il suffit de faire

```sh
!pip install numpy
```

dans celui-ci.

Des librairies (aussi appelés modules) célèbres de Python sont:

- ``numpy`` pour la manipulation de matrices.
- ``scipy`` pour les mathématiques et les algorithmes numériques.
- ``pandas`` pour la manipulation de tableaux de données (comme les dataframes du langage R).
- ``flask`` pour créer des sites webs statiques et dynamiques.
- ``PIL`` pour créer des images.
- ``BeautifulSoup`` pour parser des fichiers XML et HTML.
- ``SQLAlchemy`` pour gérer des bases de données.
- ``Requests`` pour interroger des APIs et récupérer le contenu de pages webs.
- ``matplotlib`` pour faire des graphiques.
- ``nltk`` pour faire de l'analyse textuelle.
- ``nose`` pour faire des tests unitaires.
- ``sympy`` pour faire du calcul symbolique.

Ces librairies sont *très* utilisées par les utilisateurs de Python. Avoir un connaissance de ce qui existe déjà est une bonne chose, ça ne sert à rien d'essayer de réinventer la roue alors que d'excellentes solutions existent déjà.

Nous allons maintenant voir des exemples d'utilisation de Python dans des cadres concrets intimement lié à ce qui fera pour TaxiSID.

# Programmation web

Pour cet exemple il faut commencer par télécharger et dézipper [le projet exemple de Flask](https://github.com/TaxiSID/Exemple-Flask) (cliquez sur le bouton ``Download ZIP`` sur la droite). On va utiliser cet exemple pour comprendre aussi bien comment fonctionne Flask mais aussi comment organiser un projet avec Python.

La programmation web se fait bien avec la librairie ``flask``. Après l'avoir installé avec l'utilitaire ``pip``, ouvrez le dossier ``Exemple-Flask``.

## Les templates

Le principe de Flask est de générer du contenu HTML à partir de ce qu'on appelle un *template*. Un template est tout simplement une page HTML dans laquelle on peut faire de la programmation logique (des boucles ``for``, ``if``, etc.) et de la programmation objet (héritage des pages entre elles). Les templates permettent de la programmation dite *dynamique* car on peut définir comment la page web se génère. Cela s'oppose à des pages web dites statiques qui ne changent jamais. Commencez par ouvrir ``app/templates/layout.html``:

```html
<!DOCTYPE html>
<html lang="fr">
<head>
	{% block head %}
	<link rel="stylesheet" href="static/css/style.css">
	<title>{{ title }}</title>
	<meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no'/>
	<meta charset="UTF-8">
	{% endblock %}
</head>
<body>
	<div id="content">{% block content %}{% endblock %}</div>
	<div id="footer">
		{% block footer %}
		&copy; TaxiSID
		{% endblock %}
	</div>
</body>
</html>
```

On reconnait de la syntaxe HTML classique avec des balises. On retrouve en plus ce qu'on appelle des balises *blocks* qui sont propres à Flask. Si l'on ouvre ``app/templates/layout.html``, on peut comprendre à quoi servent ces blocks:

```html
{% extends "layout.html" %}

{% block head %}
    {{ super() }}
    <style type="text/css">
        .important {
        	color: #660000;
        }
    </style>
{% endblock %}

{% block content %}

    <h1 class="important">Exemple de template avec Flask</h1>

    <ul id="annuaire">
	    {% for personne, numero in annuaire.items() %}
	        <li class="liste">{{ personne }} a comme numéro {{ numero }}</li>
	    {% endfor %}
    </ul>

{% endblock %}
```

Dans ce fichier HTML on n'utilise plus balises classiques ``<head>`` et ``<body>`` car on les a définit dans ``layout.html``. En termes de programmation objet, ``index.html`` *hérite* du contenu de ``layout.html``. On peut alors définir ce que l'on met dans les blocks qu'on a définit dans ``layout.html``.

Ne vous occupez pas trop de ce qui se passe dans ces templates, on va y revenir. Il faut juste comprendre les avantages énormes que donnent les templates:

- On n'a plus besoin de copier/coller du code redondant.
- Chaque page aura la même structure.
- On peut facilement changer la structure de toutes les pages en changeant seulement ``layout.html``.
- Définir le style du site web dans la page ``layout.html`` pour qu'il s'applique à toutes les pages.

## Les vues

Ouvrez maintenant ``app/views.py``. C'est ici que l'on définit toutes les pages web que notre application va générer. Une vue va générer une page HTML à partir d'un template (en anglais on appelle cela *render*), on va donc utiliser la fonction ``render_template`` de flask pour faire cela.

On va ensuite définir à quelle(s) URL(s) la page va être générée, ici on en choisit deux (``/`` et ``/index``). Il faut ensuite créer une fonction qui va être appelée à chaque fois qu'un utilisateur visite la page ``www.monsite.com/`` ou la page ``www.monsite.com/index``, on l'appelle ``index`` (le nom de la fonction n'est pas important). Cette fonction génère le template ``index.html`` (Flask cherche par défaut dans le dossier ``templates``) avec les variables ``title`` et ``annuaire``.

Un template peut être généré avec des variables que l'on pourra réutiliser dans la page web. Si l'on retourne à la page ``index.html``, on constate que l'on peut boucler à travers le dictionnaire qui s'appelle ``annuaire`` et ajouter des éléments ``<li>`` à la liste ``<ul>``. On constate qu'en établissant la connection entre le serveur (via le script ``views.py``) et la page web ``index.html`` avec Python et Flask beaucoup de possibilités s'offrent à nous.

Où est passée la variable ``title`` de la fonction ``index`` dans ``views.py`` lors de la génération de ``index.html``? En fait la variable ``title`` s'insère dans les balises ``<title>`` de ``layout.html`` puisque ``index.html`` a hérité du contenu de la page ``layout.html``. C'est très pratique car on aura pas à réécrire ``<title>{{ title }}</title>`` à chaque fois qu'on ajoute une nouvelle page HTML. Plus on a de pages webs et plus les templates font gagner de temps.

## Structure du projet

La structure du projet est la suivante:

    Exemple-Flask
    ├───┐ app
    │   ├───┐ static
    │   │   ├───┐ css
    │   │   │   ├───┐ lib
    │   │   │   └─── style.css
    │   │   ├───┐ data
    │   │   └───┐ js
    │   │       └───┐ lib
    │   └───┐ templates
    │   │   ├─── index.html
    │   │   └─── layout.html
    │   ├─── __init__.py
    │   └─── views.py
    ├───┐ lib
    │   └─── toolbox.py
    ├───┐ setup
    │   └─── requirements.txt
    ├─── README.md
    └─── serve.py

- Tout ce qui est relatif au site web est contenu dans le dossier ``app/``, c'est là où on l'on met les templates, les fichiers CSS, les fichiers JavaScript, les fonctions de vues etc.
- ``serve.py`` est le script principal qui va lancer le site web. ``serve.py`` est un script très simple, on y importe tout ce qui se trouve dans le dossier ``app/`` et lance l'application (par défaut sur le port 5000 de l'ordinateur). Si vous l'ouvrez dans Spyder et que vous appuyez sur la flèche verte du haut, vous pouvez ensuite rentrer ``localhost:5000`` dans la barre de recherche de votre navigateur pour voir le contenu suivant:

![Rendu de la page web](http://i.imgur.com/wCpaqOe.png?1)

- Pour qu'on puisse importer le contenu de ``app/`` dans ``script.py``, il faut créer un script appelé ``__init__.py`` dans le dossier ``app/``. En gros ``__init__.py`` définit les librairies qu'on va utiliser (``from flask import Flask``) et va importer les vues définies dans ``views.py``. Cela peut sembler un peu farfelu mais en fait c'est une façon propre de procéder et cela portera ses fruits quand le projet grandira. Une alternative plus directe aurait été de tout mettre dans ``serve.py``:

```python
from flask import Flask, render_template

app = Flask(__name__)

annuaire = {
	'Max': '0612345678',
	'Axel': '0687654321',
	'Giovanni': '0656781234',
	'Alexis': '0634561278'
}

@app.route('/')
@app.route('/index')
def index():
    return render_template('index.html', title='Accueil',
    			   annuaire=annuaire)

app.run()
```

Et ça marcherait! Cependant, bien que ça ne soit pas forcément intuitif, compartimenter son code est fortement recommandé, on s'y retrouve beaucoup mieux par la suite.

Ici le dossier ``lib/`` ne sert à rien, il est juste là pour l'exemple. On pourrait très bien imaginer que le dossier ``lib/`` contienne tout le code Python qui n'a pas à voir avec le site web mais au contraire avec, par exemple, l'analyse statistique de données. De cette façon on compartimenterait bien le site web dans le dossier ``app/`` et les analyses statistiques dans le dossier ``lib/``. Ici par exemple il y'a un script qui s'appelle ``toolbox.py`` qui contient des fonctions pour lire et écrire des fichiers JSON.

De la même façon, le dossier ``setup/`` ne sert à rien, mais on pourrait très bien imaginer qu'il puisse contenir tout le code nécessaire pour installer Python et Flask de façon à distribuer le projet à d'autres développeurs.

## Conclusion

Voilà, on a réussi à générer une page web de façon dynamique avec Python! Flask est une libraire très célèbre et vous trouverez facilement des tutoriels sur le net. On peut faire vraiment beaucoup de choses avec Flask, c'est d'ailleurs la librairie sur laquelle repose OpenBikes ([site web](http://openbikes.co/) et [repository GitHub](https://github.com/OpenBikes/Website)).

# Gestion d'une base de données

On va utiliser **PostgreSQL** pour ce projet. Vous pouvez l'installer à partir de [cette page web](http://fr.enterprisedb.com/products-services-training/pgdownload). Le téléchargement devrait inclure l'application *pgAdmin3* qui permet de visualiser et de gérer une base de données via une interface graphique. Si *pgAdmin3* n'est pas inclus dans le téléchargement de PostgreSQL vous pouvez l'installer à partir d'[ici](http://www.pgadmin.org/download/index.php).

Pour qu'on puisse communiquer avec PostgreSQL à partir de Python il faut installer la librairie ``psycopg2`` en faisant

```sh
pip install psycopg2
```

Sur Mac il faut d'abord indiquer le chemin vers l'exécutable de PostgreSQL, installer ``psycopg2`` via ``pip`` et enfin changer la librairie /usr/lib/libpq.5.dylib car elle est trop vieille avec les commandes suivantes:

```sh
export PATH="/Library/PostgreSQL/9.5/bin:$PATH"
anaconda/bin/pip install psycopg2
sudo mv /usr/lib/libpq.5.dylib /usr/lib/libpq.5.dylib.old
sudo ln -s /Library/PostgreSQL/9.5/lib/libpq.5.dylib /usr/lib
```
Si vous avez OS X El Capitan, que les commandes précédentes ne fonctionnent pas ou que vous avez un message d'erreur en important `psycopg2` dans Python, veuillez suivre les consignes suivantes : 

```sh
anaconda/bin/pip install psycopg2
sudo chown -R $(whoami):admin /usr/local
sudo ln -s /Library/PostgreSQL/9.5/lib/libssl.1.0.0.dylib /usr/local/lib/
sudo ln -s /Library/PostgreSQL/9.5/lib/libcrypto.1.0.0.dylib /usr/local/lib/
```


Une fois que vous avez bien installé pgAdmin3, ouvrez l'application et choisissez un mot de passe, cliquez ensuite sur la prise en haut à gauche comme sur l'image suivante.

![pdAdmin3](http://i.imgur.com/oXSNISa.png)

Vous pouvez ensuite rentrer des paramètres de connexion à votre guise. Vous pourrez même par la suite vous connecter au PostgreSQL d'une autre personne pour utiliser ses données! Ca sera très pratique pour le projet. Dans la suite de l'explication on utilisera les paramètres par défaut avec comme mot de passe ``houdini``.

En utilisant une librairie pour communiquer avec le SGBD (en l'occurence PostgreSQL), on va gagner en puissance car on pourra programmer des boucles pour nos insertions et plein d'autres choses. Comme on va le voir ``psycopg2`` rend l'exécution de n'importe quel programme SQL facile tel un jeu d'enfant.

De la même façon que pour l'exemple de la programmation web, vous devez télécharger et dézipper [le projet exemple de PostgreSQL](https://github.com/TaxiSID/Exemple-PostgreSQL) (cliquez sur le bouton ``Download ZIP`` sur la droite).

## Création de la base de données

Tout d'abord il faut définir nos paramètres de connexion. Une façon élégante de le faire est de créer un fichier ``connexion.json`` qui contient toutes les informations dont ``psycopg2`` a besoin pour se connecter:

	{
		"dbname": "taxisid",
		"user": "postgres",
		"password": "houdini",
		"host": "127.0.0.1",
		"port": "5432"
	}

La base de données n'est pas encore créée. On va la créer avec le script ``creation.py``:

```python
from psycopg2 import connect
from psycopg2.extensions import ISOLATION_LEVEL_AUTOCOMMIT
from lib import toolbox as tb

# On ouvre le fichier json qui contient les paramètres de connexion
params = tb.load_json('connexion.json')
# On se connecte au serveur
con = connect(
	user=params['user'],
	password=params['password'],
	host=params['host'],
	port=params['port']
)
# Nécessaire de ne pas être en mode transaction pour créer une BD
con.set_isolation_level(ISOLATION_LEVEL_AUTOCOMMIT)
# Un curseur permet d'exécuter une commande SQL avex la connexion
cur = con.cursor()
# On exécute la commande création de la base de données 
cur.execute('CREATE DATABASE {name}'.format(name=params['dbname']))
# On ferme le curseur
cur.close()
# On ferme la connexion
con.close()
```

- On commence par ouvrir le fichier JSON que l'on vient de créer. Pour cela il y'a une fonction dans ``lib/toolbox.py`` déjà définie. On importe ``toolbox.py`` avec ``from lib import toolbox as tb``.
- Ensuite on se connecte au serveur avec les paramètres que l'on a précisé dans le fichier JSON (auquel on peut accéder car on l'a chargé dans le dictionnaire ``params``). Cependant on ne précise pas le nom de la base de données puisqu'on va la créer maintenant.
- Une BD ne peut pas être créée quand on est en mode *transaction*, on l'enlève avec ``ISOLATION_LEVEL_AUTOCOMMIT`` (il n'y a pas besoin de s'en souvenir).
- On définit maintenant un curseur à partir de la connexion. C'est avec le curseur qu'on peut exécuter des programmes SQL.
- On peut maintenant exécuter le programme de création de la base avec ``cur.execute()``.
- Enfin on notifie l'utilisateur que la base de données a été créée.

## Définir une connexion

L'opération de connexion est probablement celle qui se fera le plus le long du projet. Il est donc judicieux de créer une fonction qui l'automatise à partir d'un fichier JSON contenant des paramètres de connexion. Tout comme le script ``lib/toolbox.py`` qui contient des fonctions utilisées par d'autres scripts, on va créer un script ``db.py`` qui contiendra des fonctions redondantes relatives à la base de données.

On définit la fonction de connexion comme suit:

```python
def connexion(params, transaction=True):
	'''
	Se connecte à la BD indiquée dans les paramètres.
	La fonction reçoit en entrée un fichier JSON qui a
	pour forme

	{
		"database": "taxisid",
		"user": "postgres",
		"password": "houdini",
		"host": "127.0.0.1",
		"port": "5432"
	}

	La fonction renvoit une connexion. On peut ensuite
	créer un curseur à partir de cette connexion avec
	laquelle on peut exécuter des commandes SQL.

	Le paramètre "transaction" est par défaut égal à "True"
	lorsque l'on ne veut pas être en mode "transaction".
	If faut le mettre égal à "False" si l'on veut faire
	des transactions.
	'''
	con = connect(
		database=params['dbname'],
		user=params['user'],
		password=params['password'],
		host=params['host'],
		port=params['port']
	)
	if transaction is True:
		con.set_isolation_level(ISOLATION_LEVEL_AUTOCOMMIT)
	print("Connexion à {name} réussie.".format(name=params['dbname']))
	return con
```

La fonction possède un commentaire qui fait environ les deux tiers de la fonction: c'est toujours bien de commenter son code le plus possible. La fonction prend donc en paramètre un dictionnaire contenant des paramètres de connexion. Cette fois-ci on suppose que la base de données a été créée, on va donc se connecter à celle qui est précisée dans les paramètres. On ajoute un paramètre ``transaction`` qui nous permet de choisir si on se met en mode transaction ou pas. Par défaut on ne se met pas en mode transaction (d'où le ``transaction=False``). Enfin on notifie l'utilisateur qu'il est bien connecté à la base de données.

## Créer des tables

On peut maintenant créer des tables dans la base de données. On commence par créer un script qui s'appelle ``tables.py``:

```python
from lib import db
from lib import toolbox as tb

# On ouvre le fichier json qui contient les paramètres de connexion
params = tb.load_json('connexion.json')
# On se connecte à la base de données qui est créée au préalable
conn = db.connexion(params)
# On définit un curseur pour pouvoir exécuter des commandes SQL
cur = conn.cursor()

# Création de la table "villes"
cur.execute('''
CREATE TABLE IF NOT EXISTS villes (
	nom TEXT NOT NULL PRIMARY KEY,
	pays TEXT NOT NULL,
	pib INT
);
''')
print('Table "pays" créée.')

# Création de la table "entreprises"
cur.execute('''
CREATE TABLE IF NOT EXISTS entreprises (
	id INT PRIMARY KEY NOT NULL,
	nom TEXT NOT NULL,
	age INT NOT NULL,
	adresse CHAR(50),
	salaire REAL,
	ville TEXT REFERENCES villes (nom)
);
''')
print('Table "entreprises" créée.')

# Création de la table "employes"
cur.execute('''
CREATE TABLE IF NOT EXISTS employes (
	id INT PRIMARY KEY NOT NULL,
	nom TEXT NOT NULL,
	age INT NOT NULL,
	adresse CHAR(50),
	salaire REAL,
	ville TEXT REFERENCES villes (nom),
	entreprise INT REFERENCES entreprises (id)
);
''')
print('Table "employes" créée.')
```

La connexion à la base de données est maintenant triviale. Il suffit de charger le fichier ``connexion.json`` et d'utiliser la fonction ``connexion()`` du script ``lib/db.py`` créée précédemment. On reçoit alors une connexion à la base de données. On peut définir un curseur à partir de cette connexion pour pouvoir exécuter nos programmes SQL.

Pour cet exemple on va créer une base de données toute simple, voici le schéma:

![Schéma](http://i.imgur.com/vtpScEd.png)

A cause des clés étrangères, ``Entreprises`` dépend de ``Villes``. ``Employes`` dépend de ``Villes`` et d'``Entreprises``. Il faut donc créer les tables dans le bon ordre. De la même façon il faudra peupler les tables dans le bon ordre.

La création des tables est triviale, il suffit de mettre la bonne commande SQL dans la fonction ``cur.execute()``.

## Peupler les tables

Pour insérer des valeurs dans les tables on va tout d'abord créer un fichier JSON avec des données au hasard. Ces données sont dans ``data.json`` et vous pouvez les modifier si ça vous chante. On créé ensuite un script ``insertions.py`` pour insérer ces données dans les tables que l'on vient de créer:

```python
from lib import db
from lib import toolbox as tb

# On charge le fichier JSON qui contient les paramètres de connexion
params = tb.load_json('connexion.json')
# On se connecte à la base de données qui est créée au préalable
conn = db.connexion(params)
# On définit un curseur pour pouvoir exécuter des commandes SQL
cur = conn.cursor()

# On charge les données à insérer
data = tb.load_json('data.json')

# Insertions des données dans la table "villes"
for ville in data['villes']:
	cur.execute("INSERT INTO villes VALUES (%s, %s)",
				(ville['nom'], ville['pays']))
print('Valeurs insérées dans la table "pays".')

# Insertions des données dans la table "entreprises"
for entreprise in data['entreprises']:
	cur.execute("INSERT INTO entreprises VALUES (%s, %s, %s, %s)",
				(entreprise['id'], entreprise['nom'],
			     entreprise['ca'], entreprise['ville']))
print('Valeurs insérées dans la table "entreprises".')

# Insertions des données dans la table "employes"
for employe in data['employes']:
	cur.execute("INSERT INTO employes VALUES (%s, %s, %s, %s, %s, %s)",
				(employe['id'], employe['nom'], employe['age'],
				 employe['salaire'], employe['ville'],
				 employe['entreprise']))
print('Valeurs insérées dans la table "employes".')
```

On se connecte à la base de données de la même façon que lors de la création des tables. Ensuite on va charger le fichier ``data.json`` dans un dictionnaire sur lequel on va pouvoir boucler. Le script n'est pas trop compliqué, en fait on itère à travers tous les éléments des listes contenus dans le dictionnaire. Ces listes contiennent des dictionnaires auxquels on accède aux valeurs dans ``cur.execute()`` avec un ``INSERT INTO Table VALUES (..., ..., ...)``.

On peut s'assurer que les données ont bien été insérées avec le pgAdmin3 comme sur l'image suivante.

![Vérification](http://i.imgur.com/Zr795uj.png)

Profitez-en pour vous familiariser avec l'interface de pgAdmin3, elle est très complète et assez simple à utiliser.

## Faire des requêtes sur les tables

On créé un ``requetes.py`` pour donner deux exemples de requêtes:

```python
from lib import db
from lib import toolbox as tb

# On charge le fichier JSON qui contient les paramètres de connexion
params = tb.load_json('connexion.json')
# On se connecte à la base de données qui est créée au préalable
conn = db.connexion(params)
# On définit un curseur pour pouvoir exécuter des commandes SQL
cur = conn.cursor()

# Sélectionner tous les employés
cur.execute('SELECT * FROM employes')
# On récupère les lignes qui résultent de la requête
lignes = cur.fetchall()
for ligne in lignes:
	print(ligne)

# Sélectionner les employés dans la ville où ils travaillent
cur.execute('''
			SELECT emp.id
			FROM employes emp, entreprises ent
			WHERE emp.entreprise = ent.id AND
				  emp.ville = ent.ville
			''')
# On récupère les lignes qui résultent de la requête
lignes = cur.fetchall()
for ligne in lignes:
	print(ligne)
```

Une fois que l'on s'est connecté à la base de données, les requêtes sont faciles à écrire. Ensuite, la fonction ``cur.fetchall()`` permet de récupérer le résultat de la requête sous forme de liste sur laquelle on peut boucler.

## Conclusion

Voilà pour l'introduction à PostgreSQL avec Python. Comme dit précédemment, le fait qu'on puisse gérer notre base de données à partir de Python donne de très nombreuses possibilités. Par exemple on peut encapsuler les requêtes dans des fonctions pour ensuite relier ces dernières à un formulaire web. En gros il faut se dire qu'on a accès à toutes les fonctionnalités d'un des meilleurs SGBD au monde (triggers, vues, etc.) et un langage de programmation simple qu'on peut relier à n'importe quelle source de données.

# Faire des tests

Les tests sont très importants. Un développeur devrait y passer un quart de son temps s'il veut prétendre faire du *bon* code. Je préfère tout simplement vous renvoyer vers les articles de [Sam & Max](http://sametmax.com/) sur le sujet, en plus d'être informatifs ils sont assez divertissants:

- [Partie 1](http://sametmax.com/un-gros-guide-bien-gras-sur-les-tests-unitaires-en-python-partie-1/)
- [Partie 2](http://sametmax.com/un-gros-guide-bien-gras-sur-les-tests-unitaires-en-python-partie-2/)
- [Partie 3](http://sametmax.com/un-gros-guide-bien-gras-sur-les-tests-unitaires-en-python-partie-3/)
- [Partie 4](http://sametmax.com/un-gros-guide-bien-gras-sur-les-tests-unitaires-en-python-partie-4/)
- [Partie 5](http://sametmax.com/un-gros-guide-bien-gras-sur-les-tests-unitaires-en-python-partie-5/)

Lorsque Anaconda a été installée, la librairie ``nose`` l'a été aussi. ``nose`` est un outil qui permet d'ajouter du cachet aux tests unitaires.

Imaginez que vous ayez le script de test suivant:

```python
from lib import multiply
 
def test_numbers_3_4():
    assert multiply(3,4) == 12 
 
def test_strings_a_3():
    assert multiply('a',3) == 'aaa' 
```

Dans ces tests on veut vérifier que notre fonction ``multiply`` donne bien des résultats attendus. Disons que ce script s'appelle ``tests-multiply.py``, on peut utiliser ``nose`` de la façon suivante:

```sh
nosetests tests.py
```

Cela affiche:

```sh
..
----------------------------------------------------------------------
Ran 2 tests in 0.000s
 
OK
> nosetests -v test_um_nose.py
simple_example.tests-multiply.test_numbers_3_4 ... ok
simple_example.tests-multiply.test_strings_a_3 ... ok
 
----------------------------------------------------------------------
Ran 2 tests in 0.000s
 
OK
```

Vous pouvez lire plus d'informations sur ``nose`` [ici](http://pythontesting.net/framework/nose/nose-introduction/).

# Liens

Voici une liste de références qui vous seront utiles pour bien vous préparer au projet. Certains sont en anglais mais ca n'est pas non plus du Shakespeare.

## Le langage Python

- [Un survol rapide](http://www.larsen-b.com/static/intro_python/)
- [Python pour le scientifique (très complet)](http://www.scipy-lectures.org/_downloads/PythonScientific.pdf)
- [Le cours d'OpenClassrooms](https://openclassrooms.com/courses/apprenez-a-programmer-en-python)
- [Conventions de codage](https://gist.github.com/sloria/7001839)

## Flask

- [Le cours d'OpenClassRooms](https://openclassrooms.com/courses/creez-vos-applications-web-avec-flask)
- [Le langage de template de Flask (appelé Jinja2)](http://jinja.pocoo.org/docs/dev/templates/)
- [Bonnes pratiques](https://exploreflask.com/)

## PostgreSQL

- [Documentation officielle PostgreSQL](http://docs.postgresql.fr/9.0/pg90.pdf)
- [Les triggers en PostgreSQL](http://docs.postgresqlfr.org/8.2/plpgsql-trigger.html)
- [Les vues en PostgreSQL](http://www.postgresql.org/docs/9.4/static/sql-createview.html)

# Conclusion

Vous devriez maintenant avoir les bases pour bien attaquer le projet. N'hésitez pas à envoyer un mail à **``maxhalford25@gmail.com``** si vous avez des questions.

En espérant que Python vous plaise.