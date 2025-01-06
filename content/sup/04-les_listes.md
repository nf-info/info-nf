---
title: Les listes
weight: 50
---

## Introduction

Une liste est un ensemble d'objets mis dans un ordre précis. Elles sont
définies entre crochets et les éléments sont séparés par une virgule.

#### Syntaxe

L'identificateur (le nom) d'une liste suit les mêmes règles que les
identificateurs de variables. On définit une liste vide comme suit:

```py
ma_liste = []
```

Sinon, une liste peut comporter des elements quelconques :

```py
L = [2, "hello", 3.5, True, 20, 23]
```

On peut créer une liste contenant n fois le même objet :

```py
L = [0] * 4
# Donnera la liste [0, 0, 0, 0]
```

On peut utiliser les opérateurs `+` pour la concaténation de deux
listes, et `*` pour la répétition d'une liste.

```py
T = [1, 2] * 2
# Donnera [1, 2, 1, 2]

S = ['a', 10] + [1] * 3
# Donnera ['a', 10, 1, 1, 1]
```

Pour la suite du cours, on considère la liste `L` suivante :

```py
#    0   1       2    3     4   5    <--- l'indice de chaque élément
L = [2, "hello", 3.5, True, 20, 23]
```

Les elements de la liste sont indexes a partir de 0, Pour accéder aux
elements de la liste:

```py
print(L[3])     # Affichera True
print(L[0])     # Affichera 2
print(L[1])     # Affichera hello
```

**Attention**: le premier élément correspond à l'indice 0

# Modification d'un élément

On peut modifier les elements d'une liste déjà existante comme suit :

```py
L = [1, 2, 3]

L[0] = "hello"
# La liste devient ["hello", 2, 3]

L[2] = True
# La liste devient ["hello", 2, True]

L[3] = 5
# ERREUR list index out of range.
```

# Ajout et suppression d’élément

Lorsqu'une liste existe, il est possible d'ajouter ou enlever un élément
très facilement avec les fonctions pop et append :

```py
L = [1, 2, 3]

L.append(5)         # Ajout l’élément 5 a la fin de la liste
# Donnera [1, 2, 3, 5]

L.pop(2)            # Enlève l’élément d'indice 2
# Donnera [1, 2, 5]

L.pop()             # Si on donne pas de paramètre, pop enlève le dernier
# Donnera [1, 2]

L = L + ['a', 'b']    # concaténation de deux listes
# Donnera [1, 2, 'a', 'b']
```

# Taille d'une liste

Pour obtenir la taille d'une liste, on utilise la fonction len()

```py
L = [1, 'a', True]
print(len(L))       # Affichera 3

L = [2, "hello", 3.5, True, 20, 23]
print(len(L))       # Affichera 6
```

Les elements d'une liste `L` sont donc indexes de `0` a `len(L)-1`.

Pour accéder au dernier élément d'une liste : `L[len(L)-1]`

```py
L = [2, "hello", 3.5, True, 20, 23]
x = L[len(L)-1]
print(x)        # Affichera 23
```

# Indexage négatif

Pour accéder aux elements de la liste, on peut utiliser l'indexage
négatif. Dans ce cas les elements de la liste sont indexe du dernier
élément `-1`, au premier `-len(L)`

```py
#   -6     -5     -4   -3   -2  -1
L = [2, "hello", 3.5, True, 20, 23]

print(L[-2])          # Affichera 20
```

L'indexage négatif revient a retrancher `len(L)` de l'indice positif,
par exemple l’élément d'indice 0 peut aussi être indexer par `-len(L)`.

Pour accéder au dernier élément d'une liste, on peut donc utiliser
`L[-1]` au lieu de `L[len(L)-1]`

# Méthodes et fonctions sur les listes

- `len(L)` permet d'obtenir le nombre d'elements d'une liste.

- `L.append(e)` permet d'ajouter l’élément `e` a la fin de la liste.

- `L.clear()` permet de vider la liste.

- `L.copy()` permet de faire une copy de la liste

- `L.count(e)` permet de compter le nombre d’occurrence de l’élément
  `e` dans `L`

- `L.extend(T)` permet d'ajouter tous les elements de la liste `T` a
  la fin de la liste `L`

- `L.index(e)` renvoie l'indice de l’élément `e` dans la liste `L`.
  Attention, la fonction donne une erreur si l’élément n'est pas dans
  la liste.

- `L.insert(i, e)` permet d’insérer l’élément `e` dans l'indice `i`.

- `L.pop(i)` permet d'enlever l’élément d'indice `i` et le renvoie.

- `L.remove(e)` permet d'enlever l’élément `e` de la liste si il
  existe. Attention, la fonction donne une erreur si l’élément n'est
  pas dans la liste

- `L.reverse()` permet d'inverser l'ordre des elements dans la liste

- `L.sort()` permet de trier les elements de la liste. Pour cela les
  elements doivent être du même type.

# Parcours d'une liste

On peut parcourir la liste comme suit :

```py
for i in range(len(L)):
    print("l’élément d'indice", i, "est", L[i])
```

Ou encore :

```py
for i in L:
    print("l’élément est", i)
```

**Remarque:** Si on parcourt une liste par `for x in L`, la variable `x`
va itérer sur les éléments de `L` mais on n'a pas accès à l'indice de
chaque élément. Par contre quand on utilise `for i in range(len(L))`, on
peut accéder a l’élément par `L[i]`, ainsi que son indice `i`.

# Les tranches de listes

On peut prendre une partie d'une liste définie par un indice de début
`d`, indice de fin `f`, et le pas `p` utilise, avec la syntaxe :
`L[d:f:p]` ou `L[d:f]` pour un pas de 1

#### Exemple

```py
#    0   1        2    3     4   5
L = [2, "hello", 3.5, True, 20, 23]
print(L[1:3])     # Affichera ["hello", 3.5]

```

Si on omet l'indice de début, la tranche commencera du début de la
liste. De même, si on omet l'indice de fin, la tranche finira a la fin
de la liste.

```py
print(L[3:])      # [True, 20, 23]
print(L[:2])      # [2, "hello"]

print(L[3:0:-1])  # [True, 3.5, "hello"]

print(L[::-1])    # permet d'inverser la liste
```

Si les indices début ou fin sont dans le mauvais ordre, on obtient une
liste vide :

```py
print(L[3:2])     # Affichera []
```
