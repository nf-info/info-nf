---
title: Algorithmes tri
weight: 70
---

### Énoncé du problème

On souhaite réordonner une collection d'elements suivant une relation
d'ordre déterminée. On peut, sans perte de généralité, simplifier
l’étude des différentes méthodes de tri en se limitant aux listes
d'entiers, qu'on souhaite trier par ordre croissant.

Il s'agit donc d’élaborer une fonction `tri(L)` qui prend en paramètre
une liste d'entier `L` et qui permet de trier cette liste, et de
renvoyer la liste triée.

```py
def tri(L):
    # ...
    return L

# Programme de test
L = [9, 5, 8, 1, 12, 4]
tri(L)
print(L)
```

Dans toute la suite, on pose $n = \text{ len}(L)$.

### Tri par selection

Le tri par **selection** consiste a **sélectionner** dans chaque
itération le prochain élément a placer dans la liste triée, qui est le
minimum des elements non encore tries. C'est a dire, en faisant varier
$i$ de $0$ a $n$, a chaque itération, on va remettre le $i^{\text{eme}}$
élément de la liste triée, qui est `min(L[i:n])`, a sa place `L[i]`.

#### Implémentation

```py
def tri_selection(L):
    for i in range(len(L)-1):
        indice_min = i
        for j in range(i+1,len(L)):
            if L[j] < L[indice_min]:
                indice_min = j
        L[i],L[indice_min] = L[indice_min],L[i]
```

#### Complexité

On a deux boucles imbriquées, la boucle intérieure comporte des
instructions de complexité $O(1)$, et se répète `n-i` fois, la boucle
extérieure se répète pour `i=0` a `i=n`, donc la complexité est
$O\left( n^{2} \right)$.

### Tri par insertion

Le tri par **insertion** consiste a **insérer**, un par un, les elements
de la liste non triée dans la liste triée.

#### Implémentation

```py
def insertionSort(L):
    for i in range(1, len(L)):
        cle = L[i]
        j = i-1
        while j >= 0 and cle < L[j] :
                L[j + 1] = L[j]
                j -= 1
        L[j + 1] = cle
```

#### Complexité

La complexité de la boucle intérieure dépend de l’état de la liste.

- Au meilleur des cas : La liste est déjà triée, la boucle while ne
  s'execute pas. Complexité $O(n)$.

- Au pire des cas : La liste est triée a l'ordre inverse, la boucle
  while se répète `i` fois, donc la complexité est
  $O\left( n^{2} \right)$.

### Tri a bulles

Le tri a **bulles** consiste a faire plusieurs passages de comparaisons
deux-a-deux, ou on va échanger deux elements si il ne sont pas au bon
ordre. Les elements vont se déplacer petit a petit jusqu'a trouver leurs
places. Ce déplacement global des elements ressemble aux déplacements de
**bulles** qui remontent dans un liquide.

#### Implémentation

```py
def bubbleSort(L):
    n = len(L)
    for i in range(n):
        for j in range(0, n-i-1):
            if L[j] > L[j+1]:
                L[j], L[j+1] = L[j+1], L[j]
```

#### Complexité

La complexité est $O\left( n^{2} \right)$

### Tri par fusion

Le tri par **fusion** est un tri récursif, ou on découpe la liste en
deux, on trie chaque partie a l'aide d'un appel récursif, puis on
**fusionne** les deux listes triées en une seule liste finale.

#### Implémentation

```py
def fusion(L, R):
    i = j = 0
    S = []
    while i < len(L) and j < len(R):
        if L[i] <= R[j]:
            S.append(L[i])
            i += 1
        else:
            S.append(R[j])
            j += 1
    while i < len(L):
        S.append(L[i])
        i += 1
    while j < len(R):
        S.append(R[j])
        j += 1
    return S

def tri_fusion(L):
    if len(L) <= 1:
        return L
    mid = len(L)//2
    L1 = L[:mid]
    L2 = L[mid:]

    L1 = tri_fusion(L1)
    L2 = tri_fusion(L2)
    return fusion(L1, L2)
```

#### Complexité

La complexité $C(n)$ vérifie la relation de récurrence :
$C(n) = 2C\left( \frac{n}{2} \right) + O(n)$

La complexité est donc $O\left( n\log(n) \right)$

### Tri Rapide

Le tri rapide (ou tri **pivot**) est un tri récursif qui consiste a
choisir un élément **pivot** `p` suivant lequel on découpe la liste en
deux listes : `L1` les elements inférieurs au pivot, et `L2` les
elements supérieurs au pivot, on trie alors chaque partie a l'aide d'un
appel récursif, la liste totale triée est donc : `L1 + [p] + L2`.

#### Implémentation

```py
def quick_sort(L):
    if len(L) <= 1:
        return L
    pivot = L[0]
    L1=[]
    L2=[]

    for i in range(1,len(L)):
        if L[i] <= p :
            L1.append(L[i])
        if L[i] < p :
            L2.append(L[i])
    return quick_sort(L1) + [p] + quick_sort(L2)

```

#### Complexité

On note $C(n)$ la complexité de la fonction `quick_sort(L)`, avec n =
len(L)

La boucle `for` a une complexité de $O(n)$

Le cout des appels récursifs `quick_sort(L1)` et `quick_sort(L2)` dépend
des longueurs des listes `L1` et `L2`:

- Au pire des cas :

Le pivot est le plus grand (ou plus petit) élément de la liste, `L1` et
`L2` auront les tailles `n-1` et `0`, donc : $$C(n) = O(n) + C(n-1) +
C(0)$$ Ce qui donne $$C(n) = O(n\^2)$$

- Au meilleur des cas :

Le pivot est au milieu de la liste, les listes `L1` et `L2` sont de
taille à-peu-près `n/2`, donc : $$C(n) = O(n) + 2C(n/2)$$ Ce qui donne
$$C(n) = O(nlog(n))$$
