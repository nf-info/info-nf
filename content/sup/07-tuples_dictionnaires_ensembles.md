---
title: Tuples, Dictionnaires, et Ensembles
weight: 80
---

## Introduction

Les listes et les chaînes de caractères sont une manière d'organiser et
de structurer les données. On peut également organiser les données dans
d'autres **structures de données**. Chaque structure présente différents
avantages et inconvénients suivant les situations.

## Les Tuples

**Syntaxe :**

L'identificateur (le nom) d'un tuple suit les mêmes règles que les
identificateurs de variables. On définit un tuple comme suit:

```py
T = ()
T2 = (1,)         # La virgule est importante quand il y'a un seul élément
T3 = (1, "hello", 3.14, True)
```

On peut faire les operations de concaténation `+` et de répétition `*`
sur un tuple

```py
t1 = (1, 2, 3)
t2 = t1 + (4, 5)
# Donnera (1, 2, 3, 4, 5)
t3 = t1 * 2
# Donnera (1, 2, 3, 1, 2, 3)
```

Les tuples sont indexes de la même manière que les listes

```py
#    0   1       2     3          <- indices
T = (1, "hello", 3.14, True)

```

Pour accéder aux elements du tuple :

```py
print(T[3])     # Affichera True
print(T[0])     # Affichera 1
print(T[1])     # Affichera "hello"
```

## Les tuples sont non modifiable

{{< callout type="warning" >}}
Au contraire des listes ou on peut modifier les elements, les tuples
sont **non-modifiable** 
{{< /callout >}}

```py
T = (1, 2, 3)
T[0] = 2
# ERREUR Les tuples sont non modifiable
```

## Indexage négatif

Pour accéder aux elements du tuple, on peut utiliser l'indexage négatif.
Dans ce cas les caractères de la chaîne sont indexe du dernier caractère
`-1`, au premier `-len(T)`

```py
#   -4   -3       -2     -1          <- indices
T = (1, "hello", 3.14, True)

print(T[-2])          # Affichera 3.14
```

L'indexage négatif revient a retrancher `len(T)` de l'indice positif,
par exemple l'élément d'indice 0 peut aussi être indexe par `-len(T)`.

## Méthodes et fonctions sur les tuples

- `len(T)` permet d'obtenir le nombre d'elements d'un tuple.

- `T.count(e)` permet de compter le nombre d'occurrence de l'élément
  `e` dans `T`

- `T.index(e)` donne l'indice de la première occurrence de l'élément
  `e` dans `T`

- `e in T` donne `True` si le tuple `T` contient l'élément `e`,
  `False` sinon.

## Parcours d'un tuple

On peut parcourir un tuple comme suit :

```py
for i in range(len(T)):
    print(i, T[i])
```

Ou encore :

```py
for i in T:
    print(i)
```

## Les tranches de tuples

On peut prendre des tranches de tuples comme on fait pour les listes.

Une tranche d'un tuple est définie par un indice de début `d`, indice de
fin `f`, et le pas `p` utilise, avec la syntaxe : `T[d:f:p]` ou `T[d:f]`
pour un pas de 1

**Exemple :**

```py
T = (1, "hello", 3.14, True)
print(T[1:3])     # Affichera ("hello", 3.14)

```

Si on omet l'indice de début, la tranche commencera du début du tuple.
De même, si on omet l'indice de fin, la tranche finira a la fin du
tuple. Si les indices début ou fin sont dans le mauvais ordre, on
obtient une chaîne vide.

## Les Dictionnaires

## Definition

Un dictionnaire est un ensemble de couples clé - valeur. Pour définir un
dictionnaire :

```py
d = {}    # dictionnaire vide
d1 = {"nom":"Ahmed", "age": 18 }
d2 = {1 :3, 2 : 9, 3: 81}      # Les espaces n'ont pas d'effet.
```

## Accès, modification, suppression

On peut accéder a une valeur a partir de sa clé :

```py
d1 = {"nom":"Ahmed", "age": 18 }
d2 = {1 :3, 2 : 9, 3: 81}

print(d1["nom"])      # Affichera "Ahmed"
print(d2[3])          # Affichera 81
```

On peut ajouter un nouveau couple clé-valeur ou modifier la valeur d'une
cle dans un dictionnaire comme suit :

```py
d1 = {"nom":"Ahmed", "age": 18 }
d2 = {1 :3, 2 : 6, 3: 9}

d1["age"] = 20
d1["age"] += 1
d2[4] = 12

```

Pour supprimer un couple clé-valeur :

```py
d2 = {1 :3, 2 : 6, 3: 9}

del d2[1]
# Le dictionnaire devient {2:6, 3:9}

```

## Operations sur les dictionnaires

- `len(d)` permet d'obtenir le nombre de couple clé-valeur dans un
  dictionnaire.

- `d.clear()` permet de vider le dictionnaire

- `cle in d` test si `cle` est une clé dans le dictionnaire `d`
  (retourne un boolean)

- `for cle in d` permet d'itérer sur les clés du dictionnaire

- `d.items()` donne la liste des couples clé-valeur du dictionnaire
  `d`

- `d.keys()` donne la liste des clés du dictionnaire `d`

- `d.values` donne la liste des valeurs du dictionnaire `d`

## Les ensembles

## Definition

Un ensemble est une collection d'elements sans ordre, sans répétitions.

On définit un ensemble a partir d'une liste d'elements :

```py
E = set()         # ensemble vide
F = set([1, 5, 2, 3, 1])

print(F)          # Affiche {1, 2, 3, 5}

```

## Operation sur les ensembles

- `len(E)` : permet d'obtenir le nombre d'élément de l'ensemble `E`

- `E.add(e)` : Ajoute l'élément `e` a l'ensemble `E`

- `E | F` : donne l'union $E \cup F$

- `E & F` : donne l'intersection $E \cap F$

- `E - F` : donne la différence $E - F$
