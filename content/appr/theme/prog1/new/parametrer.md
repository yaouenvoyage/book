# Paramétrer - `f(x)`

Dans ce chapitre, nous allons voir de plus près le concept de la fonction, concept que nous avons vu dès le deuxième chapitre comme façon de donner un nom à une séquence d'instructions. Ici nous allons voir comment nous pouvons ajouter un ou plusieurs paramètres à une fonction. Nous allons voir que :

- l'expression `def f(x):` permet de définir une fonction,
- un paramètre `f(par)` est une variable dans la définition de fonction,
- un argument `f(arg)` est une valeur dans l'appel de fonction.

```{question}
En Python, `def` est un raccourci pour

{f}`défoncé`  
{f}`défilé`  
{v}`définition`  
{f}`défavorisé`
```

## Paramétrer la fonction

Jusqu'à maintenant, notre carré a toujours eu la même taille.
Il serait très utile si notre nouvelle commande `carre(longueur)` pouvait dessiner des carrés de tailles différentes.
C'est possible en spécifiant un paramètre pour la fonction.
Le paramètre de la fonction est une variable locale qui est utilisée dans sa définition.

Lors de l'appel de la fonction nous donnons une valeur à la fonction.
Cette valeur placée entre parenthèses s'appelle l'**argument** de la fonction.
Ici, la fonction `carre()` est appelée successivement avec les valeurs 50, 100 et 150.

```{codeplay}
:file: def1.py
from turtle import *

def carre(longueur):
    for i in range(4):
        forward(longueur)
        left(90)
        
carre(50)
carre(100)
carre(150)
```

Une fonction peut être appelée avec une valeur numérique directe tel que `carre(50)`, mais aussi avec une valeur numérique donnée par une variable tel que `carre(x)`, obtenu par une variable d'itération sur une plage numérique donnée avec `range(start, stop, step)`.

```{codeplay}
:file: def2.py
from turtle import *

def carre(a):
    for i in range(4):
        forward(a)
        left(90)

for x in range(30, 180, 30):
    carre(x)
```

Au lieu d'imbriquer les carrés, nous pouvons aussi les dessiner les uns après les autres.
Le terme technique est de les **juxtaposer**.

```{codeplay}
:file: def3.py
from turtle import *

def carre(a):
    down()
    for i in range(4):
        forward(a)
        left(90)
    up()

up()
backward(250)
for x in range(30, 180, 30):
    carre(x)
    forward(x)
```

**Exercice** : Ecartez les carrés de 20 pixels.

## Dessiner une maison

Nous revenons à notre fonction pour dessiner une maison.

```{codeplay}
:file: def4.py
from turtle import *

def maison():
    forward (70)
    for a in (90, 45, 90, 45):
        left(a)
        forward(50)
    left(90)

backward(200)        
maison()
forward(100)
maison()
```

## Position de la maison

Maintenant nous modifions la fonction pour inclure la position de la maison comme paramètre.

```{codeplay}
:file: def5.py
from turtle import *
getscreen().bgcolor('lightgreen')
up()

def maison(x, y):
    goto(x, y)
    down()
    forward (70)
    for a in (90, 45, 90, 45):
        left(a)
        forward(50)
    left(90)
    up()

maison(0, -80)
maison(-200, 20)
maison(120, 40)
```

## Taille de la maison

Maintenant nous modifions la fonction pour inclure non seulement la position mais aussi la taille de la maison comme paramètres.

```{codeplay}
:file: def6.py
from turtle import *
getscreen().bgcolor('lightgreen')
up()

def maison(x, y, d):
    goto(x, y)
    down()
    forward (1.4 * d)
    for a in (90, 45, 90, 45):
        left(a)
        forward(d)
    left(90)
    up()

maison(-20, -80, 70)
maison(-200, 20, 50)
maison(120, 40, 40)
```

## Couleur de la maison

Maintenant nous modifions la fonction pour inclure non seulement la position, la taille mais également la couleur de la maison comme paramètres.

```{codeplay}
:file: def7.py
from turtle import *
getscreen().bgcolor('lightgreen')
up()

def maison(x, y, d, couleur):
    goto(x, y)
    down()
    fillcolor(couleur)
    begin_fill()
    forward (1.4 * d)
    for a in (90, 45, 90, 45):
        left(a)
        forward(d)
    left(90)
    end_fill()
    up()

maison(-20, -80, 70, 'lightblue')
maison(-200, 20, 50, 'yellow')
maison(120, 40, 40, 'pink')
```

## Maison avec porte

Maintenant nous modifions la fonction pour inclure non seulement la position, la taille, la couleur de la maison comme paramètres, mais nous y ajoutons aussi une porte.

```{codeplay}
:file: def8.py
from turtle import *
getscreen().bgcolor('lightgreen')
up()

def porte(d):
    for x in (1, 1.6, 1, 1.6):
        forward(d * x)
        left(90)

def mur(d):
    forward (1.4 * d)
    for a in (90, 45, 90, 45):
        left(a)
        forward(d)
    left(90)

def maison(x, y, d, col1, col2):
    goto(x, y)
    down()
    fillcolor(col1)
    begin_fill()
    mur(d)
    end_fill()

    forward(d/3)
    fillcolor(col2)
    begin_fill()
    porte(d/3)
    end_fill()
    up()

maison(-20, -80, 70, 'lightblue', 'red')
maison(-200, 20, 50, 'yellow', 'blue')
maison(120, 40, 40, 'pink', 'violet')
```

## Valeurs par défaut

Nous pouvons spécifier des valeurs par défaut.

```{codeplay}
:file: def9.py
from turtle import *
getscreen().bgcolor('lightgreen')
up()

def porte(d):
    for x in (1, 1.6, 1, 1.6):
        forward(d * x)
        left(90)

def mur(d):
    forward (1.4 * d)
    for a in (90, 45, 90, 45):
        left(a)
        forward(d)
    left(90)

def maison(x, y, d=50, col1='yellow', col2='blue'):
    goto(x, y)
    down()
    fillcolor(col1)
    begin_fill()
    mur(d)
    end_fill()

    forward(d/3)
    fillcolor(col2)
    begin_fill()
    porte(d/3)
    end_fill()
    up()

maison(-20, -80)
maison(-200, 20, col1='lime')
maison(120, 40, col2='red')
maison(-170, -140, d=80)
```

## Le coronavirus

Le nom « coronavirus » vient du latin et signifie « virus à couronne ». Son apparence sous un microscope électronique montre une frange de grandes projections bulbeuses qui évoquent une couronne solaire.

Dans la fonction `corona()` les paramètres sont :

- la distance entre projections `a`
- la longueur de la projection `d`
- le nombre de projections `n`

```{codeplay}
:file: def10.py
from turtle import *
getscreen().bgcolor('azure')
up()

def corona(a=10, d=20, n=24):
    down()
    for i in range(n):
        left(90  - 180/n)
        forward(d)
        dot()
        backward(d)
        right(90 + 180/n)
        forward(a)
    up()

corona()
```

**Exercice** : Ajoutez 3 autres virus avec d'autres valeurs pour `a`, `d` et `n`.

## Squid Game logo

Squid Game, ou Le Jeu du calmar, est une série télévisée dramatique de survie sud-coréenne de 9 épisodes, diffusée dans le monde entier en 2021 sur Netflix.
La série raconte l'histoire d'un groupe de personnes, fortement endettées, voire ruinées, qui risquent leur vie dans un jeu de survie mystérieux avec comme récompense une somme énorme.

Nous définissons une fonction `polygone(a, n)` pour dessiner le cercle, le triangle et le carré du logo.

```{codeplay}
:file: def11.py
from turtle import *
getscreen().bgcolor('peru')
width(5)
up()

def polygone(a, n):
    down()
    for i in range(n):
        forward(a)
        left(360/n)
    up()
    
backward(150)
polygone(10, 36)
forward(100)
polygone(120, 3)
forward(170)
polygone(100, 4)
```

**Exercice** : Ajoutez votre nom et vos coordonnées à la carte de visite en utilisant la fonction `write()`.

## Dessiner un pixel

Similaire à notre fonction pour dessiner un carré nous allons définir une fonction `pixel()`, mais cette fois nous ajoutons un deuxième argument :

- `taille` pour la taille du carré,
- `couleur` pour la couleur du carré.

```{codeplay}
:file: def12.py
from turtle import *

def carre(taille):
    for i in range(4):
        forward(taille)
        left(90)
        
def pixel(taille, couleur):
    fillcolor(couleur)
    begin_fill()
    carre(taille)
    end_fill()
    forward(taille)

backward(200)
for x in ('yellow', 'orange', 'red'):
    pixel(100, x)
```

## Dessiner Pikachu

Nous définissons une nouvelle fonction `ligne(couleurs)` pour dessiner une série de pixels, qui sont donnés par une liste de couleurs.
Quand le dernier pixel de la ligne est dessiné, la tortue est retournée à la position prête pour dessiner la ligne suivante.

```{codeplay}
:file: def13.py
from turtle import *

def pixel(taille, couleur):
    fillcolor(couleur)
    begin_fill()
    for i in range(4):
        forward(taille)
        left(90)
    end_fill()
    forward(taille)

taille = 50

def ligne(couleurs):
    for couleur in couleurs:
        pixel(taille, couleur)
    backward(len(couleurs) * taille)
    up()
    sety(ycor() - taille)
    down()

backward(2 * taille)
ligne(('black', 'yellow', 'yellow', 'black'))
ligne(('white', 'red', 'yellow', 'white'))
ligne(('yellow', 'yellow', 'yellow', 'yellow'))
ligne(('yellow', 'yellow', 'yellow', 'white'))
```

**Exercice** : Dessinez un autre Pokemon.
