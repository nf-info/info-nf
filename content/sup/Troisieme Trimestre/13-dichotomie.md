---
title: Méthode de dichotomie
weight: 130
draft: false
---

## Description de la méthode

Soit $f$ une fonction continue sur un intervalle $[a,b]$ avec $f(a) \times f(b) < 0$.

D'après le théorème des valeurs intermédiaires, il existe au moins une solution $\alpha \in [a,b]$ telle que $f(\alpha) = 0$.

![image](/img/dichotomie_fonction.png)

La méthode de dichotomie consiste à réduire progressivement l'intervalle de recherche en le divisant par deux à chaque étape, tout en conservant la propriété que le produit des valeurs de $f$ aux extrémités soit négatif.

### Principe de l'algorithme

1. On part d'un intervalle initial $[a_0, b_0] = [a, b]$ avec $f(a_0) \times f(b_0) < 0$.
2. On calcule le milieu $m_0 = \frac{a_0 + b_0}{2}$ de l'intervalle.
3. On évalue $f(m_0)$ :
   - Si $f(m_0) = 0$ (ou proche de 0 selon la précision souhaitée), on a trouvé une solution.
   - Si $f(a_0) \times f(m_0) < 0$, alors la solution se trouve dans $[a_0, m_0]$.
   - Si $f(m_0) \times f(b_0) < 0$, alors la solution se trouve dans $[m_0, b_0]$.
4. On obtient ainsi un nouvel intervalle $[a_1, b_1]$ de longueur moitié et qui contient toujours la solution.
5. On répète ce processus jusqu'à obtenir un intervalle suffisamment petit.

![image](/img/dichotomie_etapes.png)

À chaque itération, la longueur de l'intervalle est divisée par 2. Après $n$ itérations, la longueur de l'intervalle est donc :

$$b_n - a_n = \frac{b - a}{2^n}$$

La suite des milieux $(m_n)$ converge vers la solution $\alpha$ de l'équation $f(x) = 0$.

## Mise en œuvre pratique

Une première implémentation :

```python
def dichotomie(f, a, b, eps=1e-10):
    """
    Recherche d'un zéro de f par dichotomie
    f : fonction continue
    [a, b] : intervalle tel que f(a) * f(b) < 0
    eps : précision souhaitée
    """
    if f(a) * f(b) >= 0:
        raise ValueError("f(a) et f(b) doivent être de signes opposés")
    
    while (b - a) > eps:
        m = (a + b) / 2
        if f(m) == 0:
            return m
        elif f(a) * f(m) < 0:
            b = m
        else:
            a = m
    return (a + b) / 2
```

Ajout du paramètre `max_iter` pour limiter le nombre d'itérations :

```python
def dichotomie(f, a, b, eps=1e-10, max_iter=100):
    """
    Recherche d'un zéro de f par dichotomie
    f : fonction continue
    [a, b] : intervalle tel que f(a) * f(b) < 0
    eps : précision souhaitée
    max_iter : nombre maximal d'itérations
    """
    if f(a) * f(b) >= 0:
        raise ValueError("f(a) et f(b) doivent être de signes opposés")
    
    iter_count = 0
    while (b - a) > eps and iter_count < max_iter:
        m = (a + b) / 2
        if f(m) == 0:
            return m
        elif f(a) * f(m) < 0:
            b = m
        else:
            a = m
        iter_count += 1
    
    return (a + b) / 2
```

Variante avec affichage des itérations :

```python
def dichotomie_verbose(f, a, b, eps=1e-10, max_iter=100):
    """
    Recherche d'un zéro de f par dichotomie avec affichage des étapes
    """
    if f(a) * f(b) >= 0:
        raise ValueError("f(a) et f(b) doivent être de signes opposés")
    
    print("Iter |      a      |      m      |      b      |    f(m)    |    b-a    ")
    print("-" * 75)
    
    iter_count = 0
    while (b - a) > eps and iter_count < max_iter:
        m = (a + b) / 2
        print(f"{iter_count:4d} | {a:10.6f} | {m:10.6f} | {b:10.6f} | {f(m):10.6f} | {b-a:10.6f}")
        
        if f(m) == 0:
            return m
        elif f(a) * f(m) < 0:
            b = m
        else:
            a = m
        iter_count += 1
    
    m = (a + b) / 2
    print(f"{iter_count:4d} | {a:10.6f} | {m:10.6f} | {b:10.6f} | {f(m):10.6f} | {b-a:10.6f}")
    return m
```

## Applications

### Exemple 1 : Calcul de $\sqrt{2}$

On cherche à calculer $\sqrt{2}$ en trouvant la racine positive de l'équation $f(x) = x^2 - 2 = 0$.

```python
def f(x):
    return x**2 - 2

# Intervalle initial [1, 2] car f(1) < 0 et f(2) > 0
resultat = dichotomie(f, 1, 2)
print(f"La valeur approximative de √2 est : {resultat}")
print(f"Pour vérification, {resultat}² = {resultat**2}")
```

### Exemple 2 : Utilisation avec la bibliothèque scientifique

On peut également utiliser la fonction `bisect` du package `scipy.optimize` :

```python
from scipy.optimize import bisect

def f(x):
    return x**2 - 2

# Recherche de √2
resultat = bisect(f, 1, 2)
print(f"La valeur approximative de √2 est : {resultat}")
```

## Analyse de la convergence

La méthode de dichotomie a une convergence linéaire. À chaque itération, l'erreur est divisée par 2 :

$$|b_n - a_n| = \frac{b - a}{2^n}$$

Pour atteindre une précision $\varepsilon$, il faut environ $n$ itérations telles que :

$$\frac{b - a}{2^n} \leq \varepsilon$$

Soit :

$$n \geq \frac{\log(b-a) - \log(\varepsilon)}{\log(2)}$$

Par exemple, pour obtenir une précision de $10^{-10}$ sur un intervalle initial de longueur 1, il faut environ 34 itérations.

## Avantages et inconvénients

### Avantages
- Méthode simple à comprendre et à mettre en œuvre
- Convergence garantie pour toute fonction continue vérifiant les conditions initiales
- Robustesse (ne nécessite pas de dérivée)

### Inconvénients
- Convergence lente (linéaire)
- Nécessite de connaître un intervalle initial avec changement de signe
- Peut être inefficace pour des fonctions qui s'annulent sans changer de signe
