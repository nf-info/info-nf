---
title: Les graphes
weight: 60
---

Un graphe est un ensemble de sommets (nœuds) reliée par des arêtes
(arcs)

<figure>
<p><img src="/img/07-graph.png" style="width:50.0%" /></p>
<figcaption><p>Graphe</p></figcaption>
</figure>

$G = (V,E)$, avec $V$ l'ensemble de nœuds, $E$ l'ensemble d’arêtes.

## Notions de bases

- L'Ordre d'un graphe: c'est le nombre de nœuds du graphe :
  $\text{card}(V)$

- Graphe orienté / non-orienté

- Graphe pondéré / non-pondéré

- Degré d'un nœud, dégrée entrant, degré sortant

- Chaîne, cycle

- Chaîne eulérienne

- Chaîne hamiltonienne

## Implémentation python

En python, on peut représenter un graph de deux manières :

- Listes d'adjacence: c'est une liste qui pour chaque nœud `i` donne
  la liste des nœuds adjacent a `i`

```python
L = [[1, 2],
     [0, 2, 4],
     [0, 1, 3],
     [2, 4],
     [1, 3, 5],
     [4]
    ]
```

- Matrice d'adjacence: c'est une liste `M` a deux dimensions avec
  `M[i][j] = 1` si `i` et `j` sont liée, `0` sinon.

```python
M = [[0, 1, 1, 0, 0, 0],
     [1, 0, 1, 0, 1, 0],
     [1, 1, 0, 1, 0, 0],
     [0, 0, 1, 0, 1, 0],
     [0, 1, 0, 1, 0, 1],
     [0, 0, 0, 0, 1, 0]
    ]
```

### Graphe pondéré
Pour un graphe pondéré, on modifiera l’implémentation pour inclure la distance :

- Listes d'adjacence pondérée : les listes contiennent des tuples composé du nœud voisin, et de la distance vers ce nœud 
```python
L = [[(1, 2), (2, 2)],
     [(0, 2), (2, 4), (4, 1)],
     [(0, 2), (1, 4), (3, 3)],
     [(2, 3), (4, 1)],
     [(1, 1), (3, 1), (5, 5)],
     [(4, 5)]]
```

- Matrice d'adjacence pondérée : c'est une liste `M` a deux dimensions avec
  `M[i][j]` représente la distance entre les nœuds `i` et `j` si ils sont liée, `np.inf` sinon.

```python
M = [[0, 2, 2, np.inf, np.inf, np.inf],
     [2, 0, 4, np.inf, 1, np.inf],
     [2, 4, 0, 3, np.inf, np.inf],
     [np.inf, np.inf, 3, 0, 1, np.inf],
     [np.inf, 1, np.inf, 1, 0, 5],
     [np.inf, np.inf, np.inf, np.inf, 5, 0]
]
```
## DFS

```py
def DFS(G, visite, x):
     visite[x] = True
     print(x)
     for i in range(len(G)):
          if G[x][i] == 1 and not visite[i] :
               DFS(G, visite, i)
```

## BFS

```py
def BFS(G, x):
     visite = [False] * len(G)
     F = [x]
     visite[x] = True
     while F!=[]:

          # On visite le nœud suivant dans la file
          p = F.pop(0)
          print(p)

          for i in range(len(G)):
               if G[p][i] == 1 and not visite[i]:
                    F.append(i)
                    visite[i] = True
```


## Plus court chemin : Dijkstra

```python
def plus_proche_noeud_non_visite(distances, visite):
     min_distance = np.inf
     min_node = -1
     for i in range(len(distances)):
          if not visite[i] and distances[i] < min_distance:     
               min_distance = distances[i]
               min_node = i
     return min_node

def dijkstra(G, depart):
     n = len(G)
     distances = [np.inf] * n
     distances[depart] = 0
     visite = [False] * n

     for i in range(n):
          x = plus_proche_noeud_non_visite(distances, visite)
          visite[x] = True

          for voisin in range(n):
               if not visite[voisin] and G[x][voisin] != np.inf:
                    new_distance = distances[x] + G[x][voisin]
                    if new_distance < distances[voisin]:
                         distances[voisin] = new_distance
     return distances
```