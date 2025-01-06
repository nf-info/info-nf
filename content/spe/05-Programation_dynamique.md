# Programmation Dynamique

On considère le programme python suivant, qui permet de calculer le
énième terme de la suite fibonacci :

```python
def fibo(n):
    if (n == 0 or n == 1):
        return 1
    return fibo(n-1) + fibo(n-2)
```

Pour `n = 4` on remarque l'arbre des appels suivant :

<figure>
<p><img src="/spe/res/05-fibo_graph.png" style="width:50.0%" /></p>
<figcaption><p>Arbre d’appels récursifs.</p></figcaption>
</figure>

Cet algorithme récursif est de complexité $O\left( \varphi^{n} \right)$.
Ceci est du au fait que cet algorithme résout les mêmes sous-problèmes
plusieurs fois (`fibo(2)` par exemple, qui est appelé 2 fois).

On peut donc améliorer la solution en gardant les résultats déjà
calcules en memo. C'est la technique de **Memoisation** ou programmation
dynamique **top-down**.

```python
fibo_cache = {}

def fibo_memo(n):
    if n in fibo_cache :
        return fibo_cache[n]
    if n == 0 or n == 1 :
        fibo_cache[n] = 1
        return 1
    fibo_cache[n] = fibo_memo(n-1) + fibo_memo(n-2)
    return fibo_cache[n]
```

Une deuxième technique est de calculer les résultats par ordre croissant
des sous-problèmes, c'est l'approche **bottom-up** utilise dans
l'algorithme itérative.

```python
def fibo_iter(n):
    a, b = 1,1
    for i in range(n):
        a, b = b, a+b
    return a
```

** Caractérisation :**\
On utilise la programmation dynamique pour résoudre les problèmes qui
exhibent les 2 propriétés suivantes :

- Chevauchement des sous-problèmes

- Sous-structure optimale

## Problème 1 : Longest Common Subsequence

Étant donne deux listes `X` et `Y`, déterminer la longueur de la
sous-séquence la plus longue.

Exemple :

- `X = [1, 5, 3, 7, 2, 8, 6, 4]`

- `Y = [1, 3, 1, 2, 8, 5, 4]`

La plus longue sous-séquence est : `[1, 3, 2, 8, 4]`, qui est de
longueur `5`.

```py
memo = [ [-1 for i in range(1000) ] for i in range(1000) ]
def lcs(X, Y):
    if memo[len(X)][len(Y)] != -1 :
        return memo[len(X)][len(Y)]
    if X == [] or Y == []:
        memo[len(X)][len(Y)] = 0
        return 0
    if X[0] == Y[0]:
        s = 1 + lcs (X[1:], Y[1:])
        memo[len(X)][len(Y)] = s
        return s
    s = max ( lcs(X[1:], Y), lcs(X, Y[1:]) )
    memo[len(X)][len(Y)] = s
    return s
```

## Problème 2 : Distance Levenshtein

Étant donne deux chaînes de caractères `s1` et `s2`, on veut calculer le
nombre minimal d'operations nécessaires pour transformer `s1` en `s2`,
sachant que les operations possibles sont :

- Ajout d'un caractère

- Suppression d'un caractère

- Modification d'un caractère

Exemple :

- `s1 = "m o r o c c o"`

- `s2 = "m o n a c o"`

Dans ce cas, la distance de Levenshtein est 3; on va modifier 'r" et
'o', et supprimer 'c'.

```python
memo = {}
def lev(X, Y):
    if (len(X), len(Y)) in memo :
        return memo[(len(X), len(Y))]
    if X == '' or Y == '':
        memo[(len(X), len(Y))] = len(X) + len(Y)
        return len(X) + len(Y)
    if X[0] == Y[0]:
        s = lev (X[1:], Y[1:])
        memo[(len(X), len(Y))] = s
        return s
    s = 1 + min ( lev(X[1:], Y), lev(X, Y[1:]), lev(X[1:], Y[1:]) )
    memo[(len(X), len(Y))] = s
    return s
```

## Problème 3 : Rod cutting

Une entreprise souhaite vendre une barre métallique de taille `l`. étant
donne une liste `prix` qui associe a chaque longueur `i` le prix du
marche `prix[i]` d'une barre métallique de taille `i`, Quel est le
découpage optimale pour maximiser le gain.

```python
memo = {}
def rod_cutting(prix, l):
    if l in memo:
        return memo[l]
    if l == 0:
        memo[0] = 0
        return 0
    L = []
    for i in range(1, min(l+1, len(prix))):
        L.append(prix[i] + rod_cutting(l-i))
    s = max(L)
    memo[l] = s
    return s
```

## Problème 4 : Sac a dos (Knapsack)

- Fractional Knapsack

  ```python

  def knapsack(V, volumes, prix):
     data = [ [volumes[i], prix[i]] for i in range(len(prix)) ]
     data.sort(key=lambda x : x[1], reverse = True)
     s = 0
     i = 0
     while V > 0:
         if data[i][0] >= V :
             s += data[i][1] * V
             return s
         s += data[i][1] * data[i][0]
         V -= data[i][0]
         i+=1
     return s
  ```

- Unbound Knapsack

  ```python

  memo = {}
  def knapsack(data, V):
     if V in memo: return memo[V]
     L = []
     for i in range(len(data)):
         if data[i][0] <= V :
             L.append( data[i][1] + knapsack(data, V-data[i][0]) )
     if L == []:
         memo[0] = 0
         return 0
     memo[V] = max(L)
     return memo[V]
  ```

- 0-1 Knapsack

## Problème 5 : Longest Increasing Subsequence (LIS)

```python
memo = {}
def LIS(L, v=0):
    if (len(L), v) in memo :
        return memo[(len(L), v)]
        if L == [] :
            memo [(0, v)] = 0
            return 0
        if L[0] > v:
            a = LIS(L[1:], L[0])
        else :
            a = 0
        s = max(a, LIS(L[1:], v))
        memo [(len(L), v)] = s
        return s
```

## Problème 6 : Subset sum

```python
memo = {}
def subset_sum(L, S):
    if (len(L), S) in memo :
        return memo[(len(L), S)]
    if S == 0 :
        memo[(len(L), S)] = True
        return True
    if L == [] and S != 0:
        memo[(len(L), S)] = False
        return False
    if L[0] <= S :
        r = subset_sum(L[1:], S-L[0]) or subset_sum(L[1:], S)
    else :
        r = subset_sum(L[1:], S)
    memo[(len(L), S)] = r
    return r
```

## Problème 7 : Lattice path

## Problème 8 : Commerçant voyageur (Traveling Sales-Person)
