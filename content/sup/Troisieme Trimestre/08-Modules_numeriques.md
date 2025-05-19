---
title: Introduction aux modules NumPy et Matplotlib  
weight: 90
---
## Introduction

En Python, certains modules permettent de faciliter la manipulation de données numériques et leur représentation graphique. Les deux modules les plus utilisés dans ce domaine sont **NumPy** et **Matplotlib**. Ils sont très utilisés en science des données, en traitement d'image, en intelligence artificielle, et dans de nombreux autres domaines scientifiques.

## Le module NumPy

NumPy (Numerical Python) est une bibliothèque qui permet de manipuler des **tableaux de nombres** (appelés *ndarray*) de façon efficace.

### Importation du module

```python
import numpy as np
```

On utilise souvent l'alias `np` pour raccourcir l'écriture.

### Création d'un tableau

```python
import numpy as np
A = np.array([1, 2, 3])
B = np.array([[1, 2], [3, 4]])
```

- `A` est un tableau 1D (une ligne).
- `B` est un tableau 2D (matrice).

### Propriétés utiles

```python
A.shape      # Renvoie la taille du tableau
A.dtype      # Type des éléments (int, float, etc.)
A.ndim       # Nombre de dimensions
A.size       # Nombre total d'éléments
```

### Opérations vectorisées

Contrairement aux listes, les opérations sur les tableaux NumPy sont **automatiques sur tous les éléments**.

```python
A = np.array([1, 2, 3])
B = A + 5        # Renvoie array([6, 7, 8])
C = A * 2        # Renvoie array([2, 4, 6])
D = A ** 2       # Renvoie array([1, 4, 9])
```

Lorsque deux tableaux NumPy ont **la même forme**, on peut effectuer des opérations élément par élément, comme l'addition, la soustraction, le produit d’Hadamard (multiplication terme à terme) ou la division :

```python
A = np.array([1, 2, 3])
B = np.array([4, 5, 6])

# Addition élément par élément, comme pour les vecteurs mathématique
C = A + B        # Renvoie array([5, 7, 9])

# Soustraction élément par élément, comme pour les vecteurs mathématique
C = A - B        # Renvoie array([-3, -3, -3])

# Produit d’Hadamard : multiplication élément par élément
E = A * B        # Renvoie array([4, 10, 18])

# Division élément par élément
F = B / A        # Renvoie array([4. , 2.5, 2. ])
```


### Fonctions de création de tableaux

NumPy offre plusieurs fonctions pour créer des tableaux spécifiques :

```python
# Tableau de zéros
zeros = np.zeros(5)                # [0. 0. 0. 0. 0.]

# Tableau de uns
ones = np.ones((2, 3))             # [[1. 1. 1.]
                                   #  [1. 1. 1.]]

# Matrice identité
identity = np.eye(3)               # [[1. 0. 0.]
                                   #  [0. 1. 0.]
                                   #  [0. 0. 1.]]

# Séquence régulière
arange = np.arange(0, 10, 2)       # [0 2 4 6 8]

# Séquence régulière avec nombre d'éléments spécifié
linspace = np.linspace(0, 1, 5)    # [0.   0.25 0.5  0.75 1.  ]

# Tableau de valeurs aléatoires
random = np.random.random((2, 2))  # [[0.12345678 0.87654321]
                                   #  [0.23456789 0.98765432]]
```

### Indexation et découpage

L'indexation dans NumPy est similaire à celle des listes Python, mais avec des fonctionnalités supplémentaires pour les tableaux multidimensionnels :

```python
A = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

# Accès à un élément
A[0, 0]      # 1 (première ligne, première colonne)

# Découpage (slicing)
A[0:2, 1:3]  # [[2 3]
             #  [5 6]]

# Indexation booléenne
A > 5        # [[False False False]
             #  [False False True]
             #  [True True True]]
A[A > 5]     # [6 7 8 9]
```

### Opérations mathématiques

NumPy offre de nombreuses fonctions mathématiques :

```python
A = np.array([1, 2, 3])
np.sum(A)            # 6 (somme des éléments)
np.mean(A)           # 2.0 (moyenne)
np.max(A)            # 3 (maximum)
np.min(A)            # 1 (minimum)
np.std(A)            # Écart-type
np.exp(A)            # [2.71828183 7.3890561  20.08553692] (exponentielle)
np.log(A)            # [0. 0.69314718 1.09861229] (logarithme naturel)
np.sin(A)            # [0.84147098 0.90929743 0.14112001] (sinus)
```

### Manipulation de tableaux

NumPy permet de manipuler facilement la forme et la structure des tableaux :

```python
A = np.array([[1, 2, 3], [4, 5, 6]])

# Changement de forme
A.reshape(3, 2)      # [[1 2]
                     #  [3 4]
                     #  [5 6]]

# Transposition
A.T                  # [[1 4]
                     #  [2 5]
                     #  [3 6]]

# Aplatissement
A.flatten()          # [1 2 3 4 5 6]

# Concaténation
B = np.array([[7, 8, 9], [10, 11, 12]])
np.concatenate((A, B), axis=0)  # Concaténation verticale
                                # [[1  2  3]
                                #  [4  5  6]
                                #  [7  8  9]
                                #  [10 11 12]]

np.concatenate((A, B), axis=1)  # Concaténation horizontale
                                # [[1  2  3  7  8  9]
                                #  [4  5  6  10 11 12]]
```

### Algèbre linéaire

NumPy intègre des fonctions d'algèbre linéaire :

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Multiplication matricielle
np.dot(A, B)         # [[19 22]
                     #  [43 50]]
# ou
A @ B                # Même résultat avec l'opérateur @

# Déterminant
np.linalg.det(A)     # -2.0

# Inverse
np.linalg.inv(A)     # [[-2.   1. ]
                     #  [ 1.5 -0.5]]

# Valeurs propres
np.linalg.eigvals(A) # [-0.37228132  5.37228132]
```

## Le module Matplotlib

Matplotlib est une bibliothèque pour **tracer des courbes, des graphiques** et visualiser des données.

### Importation du module

```python
import matplotlib.pyplot as plt
```

On utilise souvent l'alias `plt`.

### Tracer une courbe simple

```python
import numpy as np
import matplotlib.pyplot as plt

# Création des données
x = np.linspace(0, 10, 100)  # 100 points entre 0 et 10
y = np.sin(x)                # Calcul du sinus de chaque point

# Création du graphique
plt.figure(figsize=(8, 4))   # Taille de la figure (largeur, hauteur) en pouces
plt.plot(x, y)               # Tracer la courbe
plt.title("Fonction sinus")  # Titre du graphique
plt.xlabel("x")              # Étiquette de l'axe x
plt.ylabel("sin(x)")         # Étiquette de l'axe y
plt.grid(True)               # Afficher une grille
plt.savefig("sinus.png")     # Sauvegarder l'image (optionnel)
plt.show()                   # Afficher le graphique
```
![Courbe simple](./res/08/sinus.png)
### Personnalisation des courbes

```python
# Plusieurs courbes sur le même graphique
plt.figure(figsize=(10, 6))
plt.plot(x, np.sin(x), label="sin(x)", color="blue", linestyle="-", linewidth=2)
plt.plot(x, np.cos(x), label="cos(x)", color="red", linestyle="--", linewidth=2)
plt.legend()  # Afficher la légende
plt.show()
```
![Plusieurs courbes](./res/08/2.png)

### Types de graphiques

Matplotlib propose de nombreux types de graphiques :

#### Nuage de points (Scatter plot)

```python
x = np.random.rand(50)
y = np.random.rand(50)

plt.figure(figsize=(8, 6))
plt.scatter(x, y, color="green", marker="o", s=100, alpha=0.5)
plt.title("Nuage de points")
plt.grid(True)
plt.show()
```
![Nuage de points](./res/08/3.png)

#### Histogramme

```python
data = np.random.normal(0, 1, 1000)  # 1000 points suivant une loi normale

plt.figure(figsize=(8, 6))
plt.hist(data, bins=30, color="purple", alpha=0.7, edgecolor="black")
plt.title("Histogramme")
plt.xlabel("Valeur")
plt.ylabel("Fréquence")
plt.grid(True)
plt.show()
```
![Histogramme](./res/08/4.png)

#### Diagramme en barres

```python
categories = ["A", "B", "C", "D", "E"]
values = [23, 45, 56, 78, 32]

plt.figure(figsize=(8, 6))
plt.bar(categories, values, color="orange")
plt.title("Diagramme en barres")
plt.xlabel("Catégorie")
plt.ylabel("Valeur")
plt.show()
```
![Barres](./res/08/5.png)

#### Diagramme circulaire (Camembert)

```python
labels = ["Groupe A", "Groupe B", "Groupe C", "Groupe D"]
sizes = [15, 30, 45, 10]
colors = ["gold", "yellowgreen", "lightcoral", "lightskyblue"]
explode = (0, 0.1, 0, 0)  # Extrude la deuxième part

plt.figure(figsize=(8, 8))
plt.pie(sizes, explode=explode, labels=labels, colors=colors, autopct="%1.1f%%", shadow=True)
plt.axis("equal")  # Pour que le cercle soit un cercle
plt.title("Diagramme circulaire")
plt.show()
```
![Camembert](./res/08/6.png)

### Sous-graphiques

Matplotlib permet de créer plusieurs graphiques dans une même figure :

```python
plt.figure(figsize=(12, 8))

# Premier sous-graphique
plt.subplot(2, 2, 1)  # (lignes, colonnes, numéro)
plt.plot(np.arange(10), np.arange(10) * 2)
plt.title("Graphique 1")

# Deuxième sous-graphique
plt.subplot(2, 2, 2)
plt.scatter(np.random.rand(10), np.random.rand(10))
plt.title("Graphique 2")

# Troisième sous-graphique
plt.subplot(2, 2, 3)
plt.bar(["A", "B", "C"], [3, 7, 2])
plt.title("Graphique 3")

# Quatrième sous-graphique
plt.subplot(2, 2, 4)
plt.hist(np.random.normal(0, 1, 100), bins=20)
plt.title("Graphique 4")

plt.tight_layout()  # Ajuste automatiquement les espaces
plt.show()
```
![sous-graphiques](./res/08/7.png)

### Graphiques 3D

Matplotlib permet également de créer des graphiques en 3D :

```python
from mpl_toolkits.mplot3d import Axes3D

# Création des données
x = np.linspace(-5, 5, 50)
y = np.linspace(-5, 5, 50)
X, Y = np.meshgrid(x, y)
Z = np.sin(np.sqrt(X**2 + Y**2))

# Création du graphique 3D
fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')

# Surface 3D
surf = ax.plot_surface(X, Y, Z, cmap='viridis', edgecolor='none')

# Personnalisation
ax.set_title("Surface 3D")
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
fig.colorbar(surf, shrink=0.5, aspect=5)  # Barre de couleur

plt.show()
```
![3D](./res/08/8.png)

## Exercices pratiques

### Exercice 1 : Manipulation de tableaux NumPy

Créez un tableau NumPy 3x3 de nombres aléatoires entre 0 et 1. Puis calculez :
1. La somme de chaque ligne
2. La somme de chaque colonne
3. Le maximum de chaque ligne
4. Le minimum de chaque colonne

### Exercice 2 : Visualisation avec Matplotlib

Créez un graphique qui montre l'évolution de trois fonctions mathématiques sur l'intervalle [0, 10] :
1. $f(x) = x^2$
2. $f(x) = x^3$
3. $f(x) = 2^x$

Utilisez des couleurs et styles de lignes différents, et ajoutez une légende.

## Ressources supplémentaires

- Documentation officielle de NumPy : [https://numpy.org/doc/stable/](https://numpy.org/doc/stable/)
- Documentation officielle de Matplotlib : [https://matplotlib.org/stable/](https://matplotlib.org/stable/)
- Galerie d'exemples Matplotlib : [https://matplotlib.org/stable/gallery/](https://matplotlib.org/stable/gallery/)
- Tutoriels NumPy : [https://numpy.org/learn/](https://numpy.org/learn/)