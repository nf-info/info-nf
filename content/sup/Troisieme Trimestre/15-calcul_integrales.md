---
title: Méthodes de calcul d'intégrales numériques
weight: 150
draft: false
---

## Introduction au calcul d'intégrales

Le calcul d'intégrales est un problème fondamental en analyse numérique. Si pour certaines fonctions simples, il est possible de calculer l'intégrale de manière exacte en utilisant des primitives, dans de nombreux cas pratiques, il est nécessaire d'utiliser des méthodes d'approximation numérique.

Nous nous intéressons au calcul numérique de l'intégrale définie :

$$I = \int_a^b f(x) \, dx$$

où $f$ est une fonction continue sur l'intervalle $[a,b]$.

![image](/img/integrale_aire.png)

Le principe des méthodes numériques est de subdiviser l'intervalle $[a,b]$ en sous-intervalles, puis d'approximer l'aire sous la courbe sur chaque sous-intervalle par des formes géométriques simples.

## La méthode des rectangles

### Principe

La méthode des rectangles consiste à approximer l'intégrale en remplaçant la fonction par une fonction constante par morceaux. On divise l'intervalle $[a,b]$ en $n$ sous-intervalles de même largeur $h = \frac{b-a}{n}$, et sur chaque sous-intervalle, on approxime la fonction par sa valeur en un point caractéristique.

On distingue trois variantes principales :

1. **Méthode des rectangles à gauche** : on utilise la valeur de la fonction à la borne gauche de chaque sous-intervalle
2. **Méthode des rectangles à droite** : on utilise la valeur de la fonction à la borne droite de chaque sous-intervalle
3. **Méthode du point milieu** : on utilise la valeur de la fonction au milieu de chaque sous-intervalle

### Formules

Soit $x_i = a + i \cdot h$ pour $i = 0, 1, 2, \ldots, n$. Les approximations de l'intégrale sont données par :

- **Rectangles à gauche** :
$$I_n \approx h \sum_{i=0}^{n-1} f(x_i)$$

![image](/img/rectangles_gauche.png)

- **Rectangles à droite** :
$$I_n \approx h \sum_{i=1}^{n} f(x_i)$$

![image](/img/rectangles_droite.png)

- **Point milieu** :
$$I_n \approx h \sum_{i=0}^{n-1} f(x_i + \frac{h}{2})$$

![image](/img/rectangles_milieu.png)

### Mise en œuvre pratique

Implémentation de la méthode des rectangles à gauche :

```python
def methode_rectangles_gauche(f, a, b, n):
    """
    Approximation de l'intégrale de f sur [a,b] par la méthode des rectangles à gauche
    f : fonction à intégrer
    [a,b] : intervalle d'intégration
    n : nombre de subdivisions
    """
    h = (b - a) / n
    somme = 0
    for i in range(n):
        xi = a + i * h
        somme += f(xi)
    return h * somme
```

Implémentation de la méthode des rectangles à droite :

```python
def methode_rectangles_droite(f, a, b, n):
    """
    Approximation de l'intégrale de f sur [a,b] par la méthode des rectangles à droite
    """
    h = (b - a) / n
    somme = 0
    for i in range(1, n+1):
        xi = a + i * h
        somme += f(xi)
    return h * somme
```

Implémentation de la méthode du point milieu :

```python
def methode_point_milieu(f, a, b, n):
    """
    Approximation de l'intégrale de f sur [a,b] par la méthode du point milieu
    """
    h = (b - a) / n
    somme = 0
    for i in range(n):
        xi = a + i * h + h/2  # Point milieu du sous-intervalle
        somme += f(xi)
    return h * somme
```

### Erreur d'approximation

Pour une fonction $f$ suffisamment régulière :
- L'erreur de la méthode des rectangles (gauche ou droite) est d'ordre $O(h)$
- L'erreur de la méthode du point milieu est d'ordre $O(h^2)$

Cela signifie que la méthode du point milieu est généralement plus précise que les méthodes des rectangles à gauche ou à droite pour un même nombre de subdivisions.

## La méthode des trapèzes

### Principe

La méthode des trapèzes consiste à approximer l'intégrale en remplaçant la fonction par une fonction affine par morceaux. Sur chaque sous-intervalle $[x_i, x_{i+1}]$, on approxime l'aire sous la courbe par un trapèze dont les hauteurs sont $f(x_i)$ et $f(x_{i+1})$.

![image](/img/trapezes.png)

### Formule

Avec les mêmes notations que précédemment, l'approximation de l'intégrale par la méthode des trapèzes est :

$$I_n \approx \frac{h}{2} \left[ f(x_0) + 2f(x_1) + 2f(x_2) + \cdots + 2f(x_{n-1}) + f(x_n) \right]$$

Ou sous forme plus compacte :

$$I_n \approx \frac{h}{2} \left[ f(a) + f(b) + 2\sum_{i=1}^{n-1} f(x_i) \right]$$

### Mise en œuvre pratique

```python
def methode_trapezes(f, a, b, n):
    """
    Approximation de l'intégrale de f sur [a,b] par la méthode des trapèzes
    f : fonction à intégrer
    [a,b] : intervalle d'intégration
    n : nombre de subdivisions
    """
    h = (b - a) / n
    somme = f(a) + f(b)  # Premier et dernier termes avec coefficient 1
    
    for i in range(1, n):
        xi = a + i * h
        somme += 2 * f(xi)  # Termes intermédiaires avec coefficient 2
        
    return (h / 2) * somme
```

Version vectorisée utilisant NumPy pour une meilleure performance :

```python
import numpy as np

def methode_trapezes_numpy(f, a, b, n):
    """
    Version vectorisée de la méthode des trapèzes utilisant NumPy
    """
    x = np.linspace(a, b, n+1)
    y = f(x)
    
    # Tous les coefficients sont 2, sauf le premier et le dernier qui sont 1
    coeffs = np.ones(n+1)
    coeffs[1:-1] = 2
    
    return (b - a) / (2 * n) * np.sum(coeffs * y)
```

### Erreur d'approximation

Pour une fonction $f$ deux fois dérivable, l'erreur de la méthode des trapèzes est d'ordre $O(h^2)$, ce qui la rend plus précise que les méthodes des rectangles à gauche ou à droite.

Plus précisément, l'erreur est donnée par :

$$E_n = -\frac{(b-a)^3}{12n^2}f''(\xi)$$

pour un certain $\xi \in [a,b]$.

## Applications et comparaison des méthodes

### Exemple : Calcul de $\int_0^1 x^2 \, dx$

Pour cette intégrale, la valeur exacte est $\frac{1}{3}$.

```python
import matplotlib.pyplot as plt
import numpy as np

def f(x):
    return x**2

a, b = 0, 1
valeur_exacte = 1/3

# Calcul avec différentes méthodes et nombres de subdivisions
n_values = [2, 4, 8, 16, 32, 64, 128]
erreurs_rectangles_gauche = []
erreurs_rectangles_droite = []
erreurs_point_milieu = []
erreurs_trapezes = []

for n in n_values:
    rect_gauche = methode_rectangles_gauche(f, a, b, n)
    rect_droite = methode_rectangles_droite(f, a, b, n)
    point_milieu = methode_point_milieu(f, a, b, n)
    trapezes = methode_trapezes(f, a, b, n)
    
    erreurs_rectangles_gauche.append(abs(rect_gauche - valeur_exacte))
    erreurs_rectangles_droite.append(abs(rect_droite - valeur_exacte))
    erreurs_point_milieu.append(abs(point_milieu - valeur_exacte))
    erreurs_trapezes.append(abs(trapezes - valeur_exacte))

# Visualisation des erreurs
plt.figure(figsize=(10, 6))
plt.loglog(n_values, erreurs_rectangles_gauche, 'o-', label='Rectangles gauche')
plt.loglog(n_values, erreurs_rectangles_droite, 's-', label='Rectangles droite')
plt.loglog(n_values, erreurs_point_milieu, '^-', label='Point milieu')
plt.loglog(n_values, erreurs_trapezes, 'd-', label='Trapèzes')
plt.grid(True)
plt.xlabel('Nombre de subdivisions (n)')
plt.ylabel('Erreur absolue')
plt.title('Comparaison des erreurs des méthodes d\'intégration numérique')
plt.legend()
plt.show()
```

![image](/img/comparaison_methodes.png)

### Observations

1. Les méthodes des rectangles à gauche et à droite ont une convergence d'ordre 1, ce qui se traduit par une pente de -1 en échelle log-log.
2. Les méthodes du point milieu et des trapèzes ont une convergence d'ordre 2, ce qui se traduit par une pente de -2 en échelle log-log.
3. Pour cette fonction particulière, la méthode du point milieu est plus précise que la méthode des trapèzes pour un même nombre de subdivisions.

## Avantages et inconvénients

### Méthode des rectangles

#### Avantages
- Simplicité de mise en œuvre
- Facilité de compréhension
- Adaptée aux cas où on ne peut évaluer la fonction qu'en des points discrets

#### Inconvénients
- Convergence lente (ordre 1 pour rectangles gauche/droite)
- Nécessite un grand nombre de subdivisions pour obtenir une bonne précision
- Ne tire pas profit de l'information sur la pente de la fonction

### Méthode des trapèzes

#### Avantages
- Meilleure précision que les rectangles à gauche/droite (ordre 2)
- Prend en compte la pente de la fonction
- Simple à implémenter et à comprendre

#### Inconvénients
- Moins précise que d'autres méthodes d'ordre supérieur (comme Simpson)
- Peut nécessiter un nombre important de subdivisions pour des fonctions à forte courbure

## Méthodes d'ordre supérieur

Pour obtenir une meilleure précision, on peut utiliser des méthodes d'ordre supérieur, comme la méthode de Simpson (ordre 4) ou les méthodes de Gauss-Legendre.

La méthode de Simpson approxime la fonction par des polynômes de degré 2 (paraboles) sur chaque sous-intervalle, ce qui donne :

$$I_n \approx \frac{h}{3} \left[ f(x_0) + 4f(x_1) + 2f(x_2) + 4f(x_3) + \cdots + 4f(x_{n-1}) + f(x_n) \right]$$

Pour un même nombre de subdivisions, la méthode de Simpson est généralement plus précise que la méthode des trapèzes.

## Conclusion

Les méthodes des rectangles et des trapèzes sont des techniques fondamentales pour le calcul numérique d'intégrales. Bien que moins précises que des méthodes plus avancées, elles restent utiles pour comprendre les principes de l'intégration numérique et peuvent être suffisantes pour des applications où une précision modérée est acceptable.

Le choix de la méthode dépend des caractéristiques de la fonction à intégrer, de la précision souhaitée et des ressources de calcul disponibles. Pour des fonctions très régulières et lorsqu'une grande précision est requise, il est préférable d'utiliser des méthodes d'ordre supérieur comme la méthode de Simpson ou les quadratures de Gauss.