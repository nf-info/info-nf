# Algorithmes Gloutons

Un algorithme glouton est un algorithme qui effectue a chaque instant,
le meilleur choix possible sur le moment, sans retour en arrière
ni anticipation des étapes suivantes, dans l'objectif d'atteindre au
final un résultat optimal.

## Problème 1 : Plus grand nombre

On souhaite écrire le plus grand nombre possible avec un ensemble de
chiffres donnes, en n'utilisant chaque chiffre qu'une seule fois.

#### Exemples :

Avec les chiffres 2, 3, 8, 6, 4, 7 le plus grand nombre est : 876432

On remarque que pour avoir le plus grand nombre possible, on place a
chaque ́étape le chiffre le plus grand a gauche (dans la position avec
le poids le plus lourd). On fait donc a chaque ́étape le meilleur choix
possible; C'est un algorithme glouton.

Donner un programme qui prend plusieurs chiffres, et renvoie le plus
grand nombre

```py
def plusGrandNombre (L) :
    return ''.join(map(str, sorted(L, reverse = True)))
```

## Problème 2 : Rendu de monnaie

On considère des pièces de monnaie de $1,2,$ et $5$ centimes. On veut
trouver la combinaison avec le nombre minimum de pièces pour obtenir
exactement $S$ centimes.

#### Exemple :

Pour $S = 7$, on choisit les pièces $5$ et $2$. Pour $S = 18$ on choisit
les pièces $5,5,5,2,1$.

Donner un programme qui prend un entier prix, et renvoie les pièces a
rendre dans l'ordre décroissant.

```py
def rendu_monnaie(S):
    R = []
    R += [5] * (S//5)
    S = S % 5
    R += [2] * (S//2)
    S = S % 2
    R += [1] * S
    return R
```

Essayons de résoudre le même problème pour le système de monnaie
$4,3,1$. Pour $S = 6$, l'algorithme glouton donne $4,1,1$. Alors que la
solution optimale est $3,3$.

title: "Attention :", \[ Les algorithmes glouton n'arrivent pas toujours
a trouver la solution globalement optimale car ils n'essayent pas toutes
les combinaisons possibles. Ils peuvent s'engager trop tôt sur certains
choix, les empêchant de trouver la meilleure solution globale par la
suite \]

## Problème 3 : Fractions Égyptiennes

Une fraction égyptienne est une fraction de numérateur égal a 1. On
souhaite ́écrire une fraction $$\frac{a}{b}$$, comme somme de fractions
égyptiennes avec des dénominateurs tous différents.

#### Exemple :

La fraction $\frac{2}{3} = \frac{1}{2} + \frac{1}{6}$\
\
La fraction $\frac{2}{5} = \frac{1}{3} + \frac{1}{15}$

La fonction prend en paramètres $a$ et $b$ et renvoie la liste des
dénominateurs des fractions qui composent la somme.

```py
def fractions_egy(a, b):
    i = 2
    R = []
    while a > 0:
        if a*i - b >= 0 :
            a, b = a*i - b, b*i
            R.append(i)
        i += 1
    return R
```

## Problème 4 : Sélection d'activités

On se donne un ensemble d'activités $a_{i}$ qui doivent chacune se
dérouler pendant un intervalle de temps $\lbrack d_{i},f_{i}\lbrack$. On
veut déterminer le maximum d’activités qu'une personne peut faire, qui
se déroulent pendant des intervalles de temps disjoints (une personne ne
peut faire qu'une activité a la fois).

On représente chaque activité par une liste de trois elements :
`[i, d, f]`, l'indice de l’activité `i`, l'heure de début `d`, et
l'heure de fin `f`.

La fonctions prend en paramètre une liste d’activité `A`, et renvoie la
liste des indices `i` des activités choisies.

```py
def select_activities(A):
    L = sorted(A, key = lambda x: x[2])
    S = [L[0][0]]
    f = L[0][2]
    for i in range(1, len(L)) :
        if L[i][1] >=  f :
            S.append(L[i][0])
            f = L[i][2]
    return S
```
