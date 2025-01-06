# Les graphes

Un graphe est un ensemble de sommets (nœuds) reliée par des arêtes
(arcs)

<figure>
<p><img src="../res/07-graph.png" style="width:50.0%" /></p>
<figcaption><p>Graphe</p></figcaption>
</figure>

$G = (V,E)$, avec $V$ l'ensemble de nœuds, $E$ l'ensemble d’arêtes.

## Notions de bases

- L'Ordre d'un graphe: c'est le nombre de nœuds du graphe :
  $\text{card}(V)$

- Graphe oriente / non-oriente

- Graphe pondéré / non-pondéré

- Degré d'un nœud, dégrée entrant, degré sortant

- Chaîne, cycle

- Chaîne eulérienne

- Chaîne hamiltonienne

## Implémentation python

En python, on peut représenter un graph de deux manières :

- Liste d'adjacence: c'est une liste qui pour chaque nœud `i` donne
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
     F = [x]
     while F!=[]:
          for i in range(len(G)):
               F


```

## Plus court chemin : Dijkstra
