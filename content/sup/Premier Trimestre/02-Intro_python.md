---
title: Introduction a Python
weight: 30
---

## Définitions

**Algorithme :**

C'est une suite finie d'opérations ou d'instructions permettant de
résoudre des problèmes, par exemple : une recette de cuisine, un manuel
d'installation, etc.

**Programme :**

Un programme est un algorithme écrit dans un langage de programmation,
destine à être exécuté par une machine, pour résoudre un problème donne.

Nous utiliserons le langage **Python**.

## Notion de variable

### Définitions

Une variable est une case mémoire qui a un **nom** (un identificateur)
et contient une **valeur** et qui est utilisé au cours d'un programme.

On l'appelle variable parce que sa valeur varie au cours de l'exécution
du programme.

**Exemple :**

En python, on crée une variable en lui affectant une valeur :

```py
a = 3
```

On définit une variable nomme `a` et on lui affecte la valeur `3`


{{< callout type="warning" >}}

L'opérateur `=` n'a pas la même signification qu'en mathématique.\
Ici, il permet d'affecter une valeur à une variable, et il n'est pas
commutatif.\
On peut l'imaginer comme suit : $a \leftarrow 3$
{{< /callout >}}


### Identificateur de variable

L'identificateur d'une variable peut contenir les lettres minuscules ou
majuscules `A-Z` et `a-z`, ainsi que les chiffres `0-9`, et le caractère
`_`. Il ne peut pas contenir d'espace, et ne doit pas commencer par un
chiffre.

#### Exemple

`ma_variable`, `Variable1`, `compteur_2` sont des noms valides.\
`ma-variable`, `3eme_compteur` ne sont **pas** des noms valides.

### Types de variables

Les valeurs contenues par les variables peuvent être de différents types
:

- Entier : en anglais "integer" ou `int`

- Réel : "floating point" ou `float`\
  La virgule est toujours notée `.` en python, e.g `a = 32.25`

- Chaîne de caractères : "string" ou `str`\
  Une chaîne est toujours entourée par des simples quotes `'` ou `""`

- Booléen : `bool` qui peut être soit `True` ou `False`

## Les commentaires

On peut ajouter dans le code python des commentaires qui ne seront pas
exécutés par python, et qui servent à décrire ou expliquer une partie du
code. Les commentaires commencent par `#`

#### Exemple

```py
# Ceci est mon premier programme Python !
var1 = 5            # ici je déclare une variable
var2 = 3.25         # une autre variable.
```

## Entrée, sortie

- Pour afficher le contenu d'une variable a l'utilisateur, on utilise
  la fonction `print()`

#### Exemple

```py
a = 3
mon_nom = "Ahmed"
print(a)          # Cette instruction affiche 3
print(mon_nom)    # Affiche Ahmed
```

- Pour lire ce que l'utilisateur écrit, on utilise la fonction
  `input()`

#### Exemple

```py
nom = input("Entrez votre nom : ")
print("Bonjour, " + nom)
```

Lors de l'exécution de ce programme, l'utilisateur va entrer son nom qui
va être enregistre dans la variable `nom` sous forme de chaîne de
caractères qu'on affiche par la suite.

## Changement de type d'une variable

On peut obtenir le type d'une variable en utilisant la fonction `type()`

#### Exemple

```py
a = 12
b = 3.25
c = "hello"
print(type(a))    # Affiche int
print(type(b))    # Affiche float
print(type(c))    # Affiche str
```

On peut transformer une chaîne de caractères comme `"15"` en un entier
(type int) `15` a l'aide de la fonction `int()`

#### Exemple

```py
a = "5"
print(type(a))    # str
x = int(a)
print(type(x))    # int
```

La fonction `int` est notamment utilisée pour obtenir un entier de chez
l'utilisateur comme suit :

```py
x = int(input("Entrez un nombre"))
```

## Opérations arithmétiques et logiques

On peut réaliser différentes opérations sur les variables.

- **Pour les nombres (type `int` ou `float`)** :

  - Addition `+`

  - Soustraction `-`

  - Multiplication `*`

  - Puissance `**`

  - Division `/`

  - Division entière `//` : Donne le quotient de la division
    euclidienne.

  - Modulo `%` : Donne le reste de la division euclidienne.

#### Exemples

```py
n = 3 * 5
m = n - 10
p = m ** 2
print(17/5)
print( 8 / 3 )          # les espaces ne font aucune différence
print( 8 % 3 )          # affiche 2
a = 7
b = 3
c = a % b               # On peut opérer sur des variables.
```

- **Pour les chaînes de caractères (type `str`)** :

  - Concaténation `+`

  - Concaténation multiple `*`

#### Exemple

```py
a = "hello "
b = "World"
print(a + b)      #Affiche "hello World"
print(3*a)        #Affiche "hello hello hello "
```

- **Pour les booléens (type `bool`)** :

  - Négation `not`

  - "ou" logique `or`

  - "et" logique `and`

#### Exemple

```py
var1 = True
var2 = False
var3 = var1 and not var2
print(var1 or var2)
```

## Opérateurs de comparaison

Les opérateurs suivants permettent de comparer deux éléments, leur
résultat et un booléen (`True` ou `False`)

- **Pour les nombres (type `int` ou `float`)** :

  - Égalité `==`

  - Différent `!=`

  - Inférieur a `<`

  - Inférieur ou égale à `<=`

  - Supérieur a `>`

  - Supérieur ou égale à `>=`

#### Exemple

```py
a = 3
b = 5
c = a <= b
print(c)              # Affichera True
print(b + 4 > 10)     # Affichera False
```

## La structure conditionnelle

Pour exécuter différentes instructions suivant la validité d'une
condition, on utilise la structure "if-else"

#### Exemple

```py
if condition :      # La variable condition est de type bool
  print("A")        # Attention à l'indentation
else :
  print("B")
```

En général, on utilise les opérateurs de comparaison comme condition
puisqu'ils renvoient un `bool`

```py
if x >= 0 :
  print(x)
else :
  print(-x)
```

On peut avoir plusieurs conditions en utilisant la forme "if-elif-else"

```py
if x>=0 and x<10 :
  print("A")
elif x>=10 and x<20 :
  print("B")
elif x < 0 :
  print("C")
else :
  print("D")
```

## Les structures itératives

Les structures itératives permettent de répéter un bloc d'instructions
plusieurs fois.

- **La structure `while`**

La structure `while` répète les instructions tant qu'une condition est
vrai.

#### Syntaxe

```py
while condition :
  print("A")
```

#### Exemples

```py
x = 10
while x > 0 :
  print("A")
  x = x - 1
```

```py
x = 0
while x < 10 :
  print(x)
  x += 1
```

- **La structure `for`**

La structure `for` est déterministe : elle répète les instructions un
nombre déterminé de fois.

#### Syntaxe

```py
for variable in collection :
  print(variable)
```

#### Exemples

```py
for i in range(10) :
  print(i)
```

```py
for i in range(10) :
  if i % 2 == 0:
    print(i)
```

```py
S = 0
for i in range(0, 101) :
  S += i
print(S)
```

La fonction `range()` peut être appelé avec 1, 2, ou 3 arguments :

- `range(5)` donnera les nombres : 0, 1, 2, 3, 4

- `range(2, 7)` donnera les nombres : 2, 3, 4, 5, 6

- `range(1, 12, 2)` donnera les nombres : 1, 3, 5, 7, 9, 11

<!-- -->

- **Le mot clé `continue`**

Le mot clé `continue` permet de sauter le reste de la boucle et passer
directement a la prochaine itération.

#### Exemple

```py
for i in range(10):
    if i%2 == 0:
        continue
    print(i)
```

Pour chaque `i` pair, le mot cle `continue` va sauter le reste des
instructions dans la boucle (notamment le `print`), et va **continuer**
d'itérer, c'est a dire passer a la prochaine itération. La boucle
n'affichera alors que les nombres impairs.

- **Le mot clé `break`**

Le mot clé `break` va immédiatement arrêter la boucle sans exécuter les
prochaines itérations.

#### Exemple

```py
for i in range(10):
    if i == 5:
        break
    print(i)
print("fin")
```

Pour `i` de 0 a 4, la boucle va afficher le nombre `i`. Pour `i=5`, le
mot clé `break` va sauter les instructions de la boucle (notamment le
`print`), et va **sortir** de la boucle, et afficher `fin`.

La boucle affichera :

`0
1
2
3
4
fin`

- **Le mot clé `pass`**

Le mot clé `pass` est une instruction qui ne fait rien.
