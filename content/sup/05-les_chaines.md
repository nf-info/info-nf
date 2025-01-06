---
title: Les chaines
weight: 60
---

## Introduction

Une chaîne de caractère est une variable qui contient du texte, un
ensemble de caractères qui se suivent dans un ordre précis. Elles sont
définies entre guillemets (double quote) `"`, ou entre apostrophes
(simple quote) `'`

#### Syntaxe

L'identificateur (le nom) d'une chaîne de caractères suit les memes
règles que les identificateurs de variables. On définit une chaîne vide
comme suit:

```py
ma_chaîne = ""
autre_chaîne = ''
```

Sinon, une chaîne de caractères peut comporter des elements quelconques
:

```py
nom = "Ahmed"
ville = 'Rabat'
age = "20"
message = "Bonjour tout le monde"
```

On peut faire les operations de concatenation `+` et de repetition `*`
sur une chaîne de caractères:

```py
ch1 = "hello "
ch2 = ch1 + "Ahmed"
# Donnera la chaîne "hello Ahmed"
ch3 = ch1 * 3
# Donnera la chaîne "hello hello hello"
```

Les chaines de caractères sont indexes de la meme manière que les listes

```py
#     01234     <--- l'indice de chaque caractère
ch = "hello"
```

Pour acceder aux elements de la chaîne de caractères:

```py
ch = "Bonjour tout le monde"
print(ch[3])     # Affichera "j"
print(ch[0])     # Affichera "B"
print(ch[7])     # Affichera " "
```

**PS**: les espaces sont aussi des caractères et ont leurs propres
indices.

# Les chaines sont non modifiable

title: \[ Attention \],

\[

Au contraire des listes ou on peut modifier les elements, les chaines de
caractère sont **non-modifiable** \]

```py
ch = "Bonjour"
ch[1] = "a"
# ERREUR Les chaines sont non modifiable
```

# Ajout d'un caractère

Pour ajouter un caractère a une chaîne, on ne peut pas modifier la
chaîne, donc on crée une nouvelle chaîne a partir de la concatenation de
la chaîne original et la chaîne a ajouter

```py
ch = "Bonjour"

ch = ch + " tout le monde"
# Donnera "Bonjour tout le monde"
```

# Taille d'une chaîne

Pour obtenir la taille d'une chaîne, on utilise la fonction len()

```py
ch = "Bonjour"
print(len(ch))       # Affichera 7

ch = " Bonjour "
print(len(ch))       # Affichera 9

```

Les elements d'une chaîne `ch` sont donc indexes de `0` a `len(ch)-1`.

Pour acceder au dernier element d'une chaîne : `ch[len(ch)-1]`

# Indexage négatif

Pour acceder aux caractères de la chaîne, on peut utiliser l'indexage
négatif. Dans ce cas les caractères de la chaîne sont indexe du dernier
caractère `-1`, au premier `-len(ch)`

```py
ch = "Bonjour"
print(ch[-2])          # Affichera "u"
```

L'indexage négatif revient a retrancher `len(ch)` de l'indice positif,
par exemple le caractère d'indice 0 peut aussi être indexe par
`-len(ch)`.

# Méthodes et fonctions sur les chaines de caractère

- `len(ch)` permet d'obtenir le nombre d'elements d'une chaîne.

- `ch.count(s)` permet de compter le nombre d’occurrence de la
  sous-chaîne `s` dans `ch`

- `ch.find(s)` renvoie l'indice de la sous-chaîne `s` dans la chaîne
  `ch`.

- `ch.replace(a, b)` renvoie une nouvelle chaîne ou la sous-chaîne `a`
  est remplace par `b`

- `ch.strip()` supprime les espaces inutiles au debut et a la fin de
  la chaîne

- `ch.lower()` convertit la chaîne en minuscule

- `ch.upper()` convertit la chaîne en majuscule

- `ch.capitalize()` convertit la premiere lettre de la chaîne en
  majuscule

- `ch.isalpha()` determine si la chaîne est constitue que de lettres
  (renvoie `True` ou `False`)

- `ch.isdigit()` determine si la chaîne est constitue que de chiffres
  (renvoie `True` ou `False`)

- `ch.isupper()` determine si la chaîne est constitue que de
  majuscules (renvoie `True` ou `False`)

- `ch.islower()` determine si la chaîne est constitue que de
  minuscules (renvoie `True` ou `False`)

# Parcours d'une chaîne

On peut parcourir une chaîne de caractère comme suit :

```py
for i in range(len(ch)):
    print(i, ch[i])
```

Ou encore :

```py
for i in ch:
    print(i)
```

# Les tranches de chaines

On peut prendre des tranches de chaines comme on fait pour les listes.

Une tranche d'une chaîne est définie par un indice de debut `d`, indice
de fin `f`, et le pas `p` utilise, avec la syntaxe : `ch[d:f:p]` ou
`ch[d:f]` pour un pas de 1

#### Exemple

```py
ch = "Bonjour"
print(ch[1:3])     # Affichera "on"

```

Si on omet l'indice de debut, la tranche commencera du debut de la
chaîne. De meme, si on omet l'indice de fin, la tranche finira a la fin
de la chaîne.

```py
ch = "Bonjour"
print(ch[3:])      # "jour"
print(ch[:2])      # "Bo"

print(ch[3:0:-1])  # "jno"

print(ch[::-1])    # permet d'inverser la chaîne "ruojnoB"
```

Si les indices debut ou fin sont dans le mauvais ordre, on obtient une
chaîne vide :

```py
print(ch[3:2])     # Affichera ""
```
