---
title: Intelligence Artificielle
weight: 80
---


## Définition

L'intelligence artificielle (IA) est l'ensemble des techniques permettant à des machines de simuler des comportements intelligents. 

**Exemples** 
- Classification d'images
- La reconnaissance vocale
- Compréhension de texte

## Problèmes de classification

Un problème de classification est un type de problème où l'objectif est de prédire la classe ou étiquette d'une donnée d'entrée, à partir d'un ensemble de données étiquetées (c'est-à-dire, des données d'entrée qui ont déjà une classification connue).

**Exemples**
- Classificateur d'images de chats/chiens
- Détecteur des emails de spam
- Classificateur des patients comme ayant une maladie ou non, en fonction de leurs symptômes ou de leurs résultats de tests médicaux.
- Reconnaissance faciale (identifier des personnes)

## Algorithme KNN (K-Nearest Neighbors)

Le **K-Nearest Neighbors (KNN)** est un algorithme simple pour faire la classification.

- Pour classer une nouvelle donnée, l'algorithme cherche les **K** exemples les plus proches dans l'ensemble des données d'entraînement, en se basant sur une métrique de distance (comme la distance Euclidienne).
- La **classe** de la nouvelle donnée sera déterminée par la classe la plus fréquente parmi ses **K** voisins les plus proches.

### Étapes a suivre  
- **On fixe un nombre K** : Le nombre de voisins à considérer.
- **On calcul la distance** entre la nouvelle donnée et toutes les données existantes.
- **On trie les distances** et on considère les **K** plus petites distances.
- **Attribuer la classe** à la nouvelle donnée, c'est la classe la plus fréquente sur les K voisins les plus proches.

### Exemple

On va utiliser le dataset Iris qui a été publié en 1935 par le biologiste Edgar Anderson. Ce dataset contient les mesures de 150 échantillons de fleurs répartis en 3 classes d'iris (Iris-setosa, Iris-versicolor et Iris-virginica), Les 4 caractéristiques mesurées sont : la longueur et la largeur du sépale, ainsi que la longueur et la largeur du pétale. 

On va implémenter l'algorithme KNN pour permettre de prédire l'espèce d'une fleur d'iris en fonction de ses caractéristiques, en utilisant les k voisins les plus proches dans le jeu de données.

Pour commencer, on va lire le csv pour en tirer les valeurs des caractéristiques (features) `X` et les classes associées `y`

```python
def lire_csv(filename):
    data = np.genfromtxt(filename, delimiter=',', dtype=str)

    X = data[:, :-1].astype(float)  # Toutes les colonnes sauf la dernière (les features)
    y = data[:, -1]                 # les classes
    
    return X, y
```

Puis nous allons visualiser les différentes caractéristiques du dataset Iris les unes par rapport aux autres à l'aide de `plt.scatter`. Ces graphes vont nous permettre de mieux comprendre la distribution des données.

```py
X, y = lire_csv('iris.csv')

label_map = {'Iris-setosa': 0, 'Iris-versicolor': 1, 'Iris-virginica': 2}

y_numeric = np.array([label_map[label] for label in y])
colors = ['r', 'g', 'b']

fig, axes = plt.subplots(4, 4, figsize=(12, 12))
axes = axes.flatten()

feature_pairs = [(i,j) for i in range(4) for j in range(4)]

for i, (x_idx, y_idx) in enumerate(feature_pairs):
    ax = axes[i]
    
    for label_idx, color in zip(range(len(label_map)), colors):
        label_data = X[y_numeric == label_idx]
        ax.scatter(label_data[:, x_idx], label_data[:, y_idx], label=list(label_map.keys())[label_idx], color=color, s=20)

plt.tight_layout()
plt.show()
```

On obtient le graphe suivant :
<figure>
<p><img src="../res/08_iris.png" style="width:100.0%" /></p>
<figcaption><p>Distribution suivant les différentes caractéristiques</p></figcaption>
</figure>


A partir de ce graphe, on remarque que pour les caractéristiques 3 et 4, la distribution de chaque classe est assez regroupé permettant de mieux différencier et délimiter les différentes classes. On dira alors que les caractéristiques "longueur des pétales" et "largeur des pétales" sont les plus importantes pour la classification. On peut alors simplifier le problème en se limitant a ces deux features.

```py
```

## Algorithme K-means

Cette fois, l'ensemble des données n'est pas étiquetée, et on souhaite déterminer les classes.
L'algorithme K-means permet de trouver une partition d'un ensemble de données en plusieurs groupes ou clusters, de façon a ce que les elements de chaque groupe soient aussi similaires que possible

Les étapes de l'algorithme:
- On fixe k, le nombre de clusters souhaités
- On crée k points aléatoires qu'on appel centroids dans l'espace des points de données
- On répète les étapes suivantes :
  - On associe chaque point de donnée au centroid le plus proche.
  - On déplace les centroids vers la moyenne de leur groupe

Quand l'algorithme converge, les centroids ne se déplacent plus, et on obtient la classification des données 


```python
import numpy as np
import matplotlib.pyplot as plt
from math import sqrt

def lire_csv(filename):
    data = np.genfromtxt(filename, delimiter=',', dtype=str)

    X = data[:, 2:-1].astype(float)  # Toutes les colonnes sauf la dernière (les features)
    
    return X

X = lire_csv('iris.csv')
# print(X)

plt.scatter(X[:, 0], X[:, 1])
plt.show()

def distance(P, Q):
    S = 0
    for i in range(len(P)):
            S += (P[i]-Q[i])**2
    return sqrt(S)

def moyenne(X, classe, k):
    centroids = []
    for j in range(k):
        somme = np.zeros(X[0].shape)
        n = 0
        for i in range(len(X)):
            if classe[i] == j:
                n += 1
                somme += X[i]
        centroids.append(somme/n)
    return np.array(centroids)

def k_means(X, k):

    centroids = []
    for i in range(k):
        center = np.array([7, 3]) * np.random.random(2) + np.array([1, 0])
        centroids.append(center)
    centroids = np.array(centroids)

    plt.scatter(X[:, 0], X[:, 1])
    plt.scatter(centroids[:, 0], centroids[:, 1], color="red")
    plt.show()

    n = 100
    while n > 0 :
        classe = []
        for i in range(len(X)):
            m = np.inf
            centre_le_plus_proche = 0
            for j in range(k):
                d = distance(X[i], centroids[j])
                if d < m:
                    m = d
                    centre_le_plus_proche = j
            classe.append(centre_le_plus_proche)

        # plt.scatter(X[:, 0], X[:, 1], c=classe)
        # plt.scatter(centroids[:, 0], centroids[:, 1], color="red")
        # plt.show()

        centroids = moyenne(X, classe, k)

        # plt.scatter(X[:, 0], X[:, 1], c=classe)
        # plt.scatter(centroids[:, 0], centroids[:, 1], color="red")
        # plt.show()

        n-=1

    plt.scatter(X[:, 0], X[:, 1], c=classe)
    plt.scatter(centroids[:, 0], centroids[:, 1], color="red")
    plt.show()
```
