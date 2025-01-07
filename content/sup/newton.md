---
title: Méthode de newton
weight: 90
draft: true
---

### Description de la méthode

Soit $f$ une fonction réelle.  
On cherche la solution $\alpha$ de l'équation $f(x) = 0$
![image](../res/cubic.png)

On part d'une valeur $x_0$ au hasard (sous
certaines conditions) et on trace la tangente $T_1$ à la courbe
$\mathcal{C}_f$ de $f$ en $x_0$

![image](../res/01.png)

L'abscisse $x_1$ du point d'intersection de la tangente $T_1$ avec l'axe
des abscisses est une valeur approchée de la solution $\alpha$

Quelle est la formule de $x_1$ en fonction de
$x_0$ ?

On réitère ce même principe un certain nombre
de fois avec $x_n$ et la tangente $T_n$ au point d'abscisse $x_{n-1}$.  
On obtient donc une suite $\left ( x_n \right )_{n}$ qui converge vers
la solution $\alpha$



![image](../res/03.png)


![image](../res/05.png)


![image](../res/07.png)


![image](../res/09.png)

La suite $\left ( x_n \right )_{n}$ est donc
définie par la relation de récurrence :

A retenir $$x_n = x_{n-1} - \frac{f(x_{n-1})}{{f}'(x_{n-1})}$$

### Mise en œuvre pratique

Une première implémentation : 

```python
def newton(f, df, x0, eps=2**-50):
    x = x0
    while ( abs(f(x)) > eps ):
        x = x - f(x) / df(x)
    return x
```

Ajout du paramètre ```max_iter``` :

```python
def newton(f, df, x, eps=2**-50, max_iter = 100):
    i = 0
    while ( abs(f(x)) > eps and i < max_iter):
        x = x - f(x) / df(x)
        i = i + 1
    return x
```

### Applications

On souhaite calculer une valeur approchée de $\sqrt{2}$.  
On construit donc la fonction $f(x) = x^2 - 2$ qui a pour racines
$\sqrt{2}$  et $-\sqrt{2}$  
La racine obtenue dépendra du choix de $x_0$

```python
def newton(f, df, x, eps=2**-50, max_iter = 100):
    i = 0
    while ( abs(f(x)) > eps and i < max_iter):
        x = x - f(x) / df(x)
        i = i + 1
    return x
    
def f(x):
    return x**2 - 2
def df(x):
    return 2*x
    
print(newton(f, df, 1))
```

On peut également utiliser la fonction newton du package
scipy.optimize

```python
from scipy.optimize import newton

def f(x):
    return x**2 - 2
def df(x):
    return 2*x
    
print(newton(f, 1, df))
```
