---
title: Complexité
weight: 10
---

La complexité d'un algorithme est une mesure des ressources nécessaires
à son exécution, il y a deux ressources principales:

- Complexité spatiale: quantité de mémoire requise.

- Complexité temporelle: temps de calcul à prévoir.

Le but de ces mesures est de comparer les algorithmes pour pouvoir
identifier l'algorithme le plus efficace.

On ne mesure pas les valeurs exactes (le nombre d'octets nécessaires ou
le nombre de secondes) mais uniquement des ordres de grandeurs en
fonction des paramètres d'entrée.

**Exemple :**

On souhaite comparer deux algorithmes qui permettent de déterminer si un
entier naturel `n` est premier ou pas:

- Pour cette première version on test si:
  $$\left( \forall i \in ⟦2,n⟦ \right) i \mid n$$

```python {linenos=table,linenostart=1,filename="version1.py"}
#
      def test_premier_version_1(n):
        flag = True
        for i in range(2,n):
            if (n % i == 0):
                flag = False
        return flag

```

- Pour la deuxième version on test si:

$$\left( \forall i \in ⟦2,\sqrt{n}⟧ \right) i \mid n$$

```python {linenos=table,linenostart=1,filename="version2.py"}
from math import sqrt, ceil
def test_premier_version_2(n):
    flag = True
    for i in range(2, ceil(sqrt(n))):
        if (n % i == 0):
            flag = False
    return flag

```


**Quelle version est la plus rapide ?**

L'intuition nous dis que la deuxième version est la plus rapide, mais
pour mesurer ça, on s'appuie sur la notion de **complexité**.

## Calcul de Complexité

### Instructions élémentaires

Il est nécessaire de préciser les instructions élémentaires disponibles,
c'est-à-dire les opérations de coût constant:

- opérations arithmétiques et logiques: `a + b`, `a - b`, `a / b`,
  `a and b`

- comparaisons de données élémentaires: `a < b`, `a == b`

- transferts de données **simples**: `a = 42`

- instructions de contrôle: `if`, `else`, `while`, `for`, `return`,
  `def`

### Méthode de calcul

On énuméré le nombre d'instructions élémentaires qui seront exécutées
dans l'algorithme, en utilisant les règles suivantes:

**Règles :**

Pour les boucles `for`:

```py
for i in range(n):      # 1
    # Bloc a            # cout: T_a(i)
```

La complexité totale de la boucle est de:
$$C(n) = O(1) + O\left( \sum_{i = 0}^{n - 1}T_{a}(i) \right)$$ Pour les
boucles `while`:

```py
while (condition):      # 1
    # Bloc a            # T_a(i)
```

Il n'y a pas de méthode sur, mais on essaye de trouver le nombre
d'itérations totales que fera la boucle, selon la condition. Ce nombre
dépend des entrées, notant le $f(n)$

La complexité est donc:
$$C(n) = O(1) + O\left( \sum_{i = 0}^{f(n)}T_{a}(i) \right)$$

Pour les conditions:

```py
if (condition_1):       # 1
    # Bloc a            # T_a(n)
elif (condition_2):     # 1
    # Bloc b            # T_b(n)
else:                   # 1
    # Bloc c            # T_c(n)
```

Puisqu'on s'intéresse a la complexité **au pire des cas**, on utilise le
max des différentes complexités des branches:
$C(n) = O(1) + O\left( \max\left\lbrack T_{a}(n),T_{b}(n),T_{c}(n) \right\rbrack \right)$

**Exemple :**

```py
def test_premier_version_1(n):      # 1
    flag = True                     # 1
    for i in range(2, n):           # 1
        if (n % i == 0):            # 1
            flag = False            # 1
    return flag                     # 1
```

Après avoir énumérer les instructions élémentaire ci-dessus, on calcul
la complexité $C(n)$:
$$C(n) = O(1) + O(1) + O(1) + \sum_{i = 2}^{n - 1}O(1)$$
$$C(n) = O\left( 3 + (n - 2) \right)$$ On utilise la propriété suivante:
$$f = o(g) \Rightarrow O(f + g) = O(g)$$ On obtient: $$C(n) = O(n)$$

## Classes de complexité

Le graphe suivant montre les comportements asymptotiques des différentes
classes de complexité:

<figure>
<p><img src="../res/01-graph.png" style="width:80.0%" /></p>
<figcaption><p>Classe de complexité</p></figcaption>
</figure>

Pour estimer le temps d'exécution $T$ d'un algorithme pour une taille
d'entrée $n$, on se base sur sa complexité $C(n)$ qui représente le
nombre d'instructions exécutées, et on utilise la fréquence du
processeur $f$ qui est le nombre d'instructions exécutées par seconde.
$$T = \frac{C(n)}{f}$$

Pour un processeur de fréquence 1GHz on obtient les valeurs suivantes:

<figure>
<p><img src="../res/01-complexité_temps.png" style="width:100.0%" /></p>
<figcaption><p>Temps d'exécution</p></figcaption>
</figure>

## Exercices

Calculez les complexités des fonctions suivantes:

```py
def f1(n):
    for i in range (n):
        for j in range(n):
            print("Hello")
```

```py
def f2(n):
    for i in range(n):
        for j in range(i):
            print("Hello")
```

```py
def f3(n):
    k=n
    while (k > 1):
        k = k // 2
```

```py
def f4(n, m):
    while n + m > 1:
        if (n + m) % 2 == 0:
            n -= 1
        else:
            m -= 1
```

```py
def f5(n):
    for i in range(n*n):
        for j in range(i):
            print ("Hello")
```

```py
def f6(n, m):
    for i in range(n):
        t = 1
        while t < m:
            print ("Hello")
            t = t * 2
```

```py
def f7(n, L):
    for i in range(n):
        if i % 2 == 0:
            sorted(L)
```

{{< callout type="warning" >}}
 Les instructions suivantes ne sont pas
élémentaire:

- recherche dans une liste; `x in L`, `L.index(x)`, `L.remove(x)`

- transferts de données composées; `T = L.copy()`, `chaîne = f.read()`

En général, il faut se méfier de tout appel a des fonctions prédéfinis.
{{< /callout >}}


## Complexité des fonctions récursives

On applique les mêmes étapes:

**Exemple :**

On note $C(n)$ la complexité de la fonction suivante:

```py
def factorielle(n):                 # 1
    if n <= 1:                      # 1
        return 1                    # 1
    return n * factorielle(n-1)     # 1 + C(n-1)
```

Le coût de l'appel récursif `factorielle(n-1)` est $C(n - 1)$.

On calcul alors la complexité $C(n)$:

$$C(n) = O(1 + 1 + 1) + C(n - 1)$$ Et on a
$$C(1) = O(1 + 1 + 1) = O(1)$$

On peut alors montrer par récurrence que: $$C(n) = O(n)$$

**Règles :**

Pour les fonctions récursives, le calcul de complexité donne souvent une
formule de récurrence, il faut donc la résoudre pour trouver la formule
du terme général.

{{< callout type="warning" >}}
On peut s'appuyer sur le **master théorème** pour trouver rapidement la
formule générale. mais la preuve de ce théorème est hors-programe 
{{< /callout >}}

Pour 
$$ \begin{cases}
T(n) = aT\left( \frac{n}{b} \right) + O\left( n^{k} \right) \\\\
T(1) = O(1)
\end{cases} $$


 On compare $k$ avec $log_{\left\( b \right\)}(a)$:

$$
T(n) = \begin{cases}
O\left( n^{k} \right) & \text{ si }\log_{b}(a) < k \\\\
O\left( n^{k}\log_{b}(n) \right) & \text{ si }\log_{b}(a) = k \\\\
O\left( n^{\log_{b}(a)} \right) & \text{ si }\log_{b}(a) > k
\end{cases}$$ 

## Exercices

``` py
def f8(n):
    if (n == 0):
        return 1
    return f8(n-1) + f8(n-1)
```

``` py
def f9(n):
    if (n == 0):
        return 1
    résultat = f9(n-1)
    return résultat + résultat
```

``` py
def puissance_v1(a,b):
    if (b == 0):
        return 1
    return a * puissance_v1(a, b-1)
```

``` py
def puissance_v2(a,b):
    if (b == 0):
        return 1
    if (b % 2 == 0):
        return puissance_v2(a, b//2) ** 2
    if (b % 2 == 1):
        return a * puissance_v2(a, b//2) ** 2
```

``` py
def fibonacci(n):
    if (n <= 1):
        return 1
    return fibonacci(n-1) + fibonacci(n-2)
```


