---
title: Les fonctions
weight: 40
---

## Introduction
Pour mieux structurer nos programmes et les rendre réutilisables, on
les regroupe dans des unités appelée "fonctions".

Une fonction est donc un "bout de code", un ensemble d'instructions qui
est exécutée et renvoie un résultat a partir des donnes d’entrée :

<figure>
<p><img src="../res/03-fonction.png" style="width:40.0%" /></p>
<figcaption><p>Schema d’une fonction python</p></figcaption>
</figure>

# Syntaxe

Pour créer une fonction, on utilise la syntaxe suivante:

```py
def ma_fonction(x, y, z):
    # Bloc d'instructions
```

- `def` est un mot clé qui permet de commencer la definition d'une
  fonction.

- Le nom d'une fonction obéit aux mêmes règles que les noms de
  variables.

- Les paramètres de la fonctions sont mis entre parenthèse

#### Exemple

```py
def double(x):
    print(x * 2)
```

Le code ci-dessus défini une fonction qui prend une variable `x` et qui
affiche la valeur `x * 2`

title : \[ Attention :\], \[ L'execution de ce code ne va **rien**
faire, parce qu'il s'agit uniquement d'une definition de la fonction.
Pour l’exécuter il faut **appeler** la fonction. \]

L'appel de la fonction se fait comme suit :

```py
double(3)
```

Ce code fait appel a la fonction `double` avec le paramètre `x = 3`. La
fonction va s’exécuter et afficher `6`.

En générale on évite d’écrire des fonctions qui affichent leur résultat,
et on opte plutôt pour des fonctions qui **renvoie** le résultat a
l'aide du mot clé `return`.

#### Exemple

```py
def cube(x):
    return x * x
```

L'appel a cette fonction va **renvoyer** le résultat `x * x` On peut
alors récupérer le résultat en l'affectant a une variable comme suit :

```py
y = cube(3)
```

La fonction va être exécutée pour la valeur `x=3`, va calculer le
résultat et le renvoyer, pour qu'il soit affectée a la variable `y`.

# Procédure

Lorsqu’une fonction ne contient pas le mot clé `return`, on dit qu'elle
ne renvoie rien. En réalité, python va plutôt renvoyer une valeur
spéciale appelée `None`.

On appel les fonctions qui ne renvoient rien des **procédures**.

# Paramètre facultatif

On peut faire en sorte d'avoir une fonction qui peut être appelée avec
ou sans un paramètre. Ce paramètre est alors facultatif, et on doit
définir la valeur par défaut de ce paramètre.

#### Exemple

```py
def ma_fonction(x, y=10):
    print(x, y)
```

On peut appelée cette fonction en lui donnant 1 ou 2 paramètre :

```py
ma_fonction(5, 6)       # affiche "5 6"
ma_fonction(3)          # affiche "3 10"
```

# Variable locale vs variable globale

Considérons le code suivant:

```py
def test():
  a = 6

a = 5
test()
print(a)
```

Ce code est contre-intuitive, contrairement a ce qu'on peut croire, il
affiche la valeur `5`

Voici en detail ce qui se passe :

- Les lignes 1 et 2 ne vont rien faire puisqu'il s'agit d'une
  definition de fonction.

- La ligne 4 déclare une variable appelée `a` ayant la valeur `5`

- La ligne 5 fait appel a la fonction `test`, l’interpréteur va alors
  exécuter la ligne 2.

- La ligne 2 déclare une **nouvelle** variable appelée `a` ayant pour
  valeur `6`

Même si les deux variables ont le même nom, la première est **globale**,
c'est-a-dire accessible depuis n'importe ou dans le code, alors que la
deuxième est **locale** a la fonction `test`

- La fonction étant exécutée, on revient a la ligne 6

- La ligne 6 va afficher la variable `a`, puisqu'on est a l’extérieur
  de la fonction, la variable locale a la fonction `test` n'est plus
  accessible, on va donc afficher la variable `a` globale, qui
  contient toujours la valeur `5`

# Fonction anonyme

Python permet de manipuler les fonctions comme on manipule des
variables, on peut donc envoyer une fonction en paramètre a une autre
fonction, et on peut créer des fonction anonyme, qui n'ont pas de nom.

#### Syntaxe

```py
f = lambda x : x * x
g = lambda y : y + 2

h = lambda x : g(f(x))
```
