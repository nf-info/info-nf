---
title: Algorithme heuristique
weight: 70
---

## Introduction

Un algorithme heuristique est un algorithme qui cherche à trouver une solution optimale ou quasi-optimale à un problème donné, mais en utilisant une approche approximative plutôt qu'une recherche exhaustive. Ces algorithmes sont souvent utilisés dans des problèmes où une solution exacte prendrait trop de temps à calculer ou serait trop coûteuse en ressources.

Les heuristiques sont des fonctions qui servent de guides pour orienter la recherche vers des solutions prometteuses. Elles évaluent la "proximité" d'un état donné à la solution finale, et permettent de prioriser certains chemins dans la recherche.

## Exemple : Algorithme A* pour le plus court chemin

L'algorithme A* illustre parfaitement le concept d'algorithme heuristique. Il est utilisé pour trouver le plus court chemin entre deux points dans un graphe, en utilisant une heuristique pour guider la recherche.

### Principe de fonctionnement

1. L'algorithme maintient deux ensembles de nœuds :
   - `open_set` : les nœuds à explorer
   - `closed_set` : les nœuds déjà explorés

2. Pour chaque nœud, il calcule deux scores :
   - `g_score` : le coût réel du chemin depuis le départ
   - `h_score` : l'estimation (heuristique) de la distance jusqu'à l'arrivée
   - `f_score = g_score + h_score` : le score total estimé

3. À chaque étape, il choisit le nœud avec le plus petit `f_score` dans `open_set`

```python
def a_star(start, goal, graph, heuristic):
    open_set = {start}
    closed_set = set()
    came_from = {}
    g_score = {start: 0}
    f_score = {start: heuristic(start, goal)}
    
    while open_set:
        current = min(open_set, key=lambda x: f_score.get(x, float('inf')))
        
        if current == goal:
            return reconstruct_path(came_from, current)
            
        open_set.remove(current)
        closed_set.add(current)
        
        for neighbor in graph[current]:
            if neighbor in closed_set:
                continue
                
            tentative_g_score = g_score[current] + graph[current][neighbor]
            
            if neighbor not in open_set:
                open_set.add(neighbor)
            elif tentative_g_score >= g_score.get(neighbor, float('inf')):
                continue
                
            came_from[neighbor] = current
            g_score[neighbor] = tentative_g_score
            f_score[neighbor] = g_score[neighbor] + heuristic(neighbor, goal)
    
    return None
```

### Exemple d'utilisation

```python
# Exemple de graphe
graph = {
    'A': {'B': 4, 'C': 3},
    'B': {'A': 4, 'D': 5},
    'C': {'A': 3, 'D': 6},
    'D': {'B': 5, 'C': 6}
}

# Heuristique simple : distance euclidienne
def heuristic(node, goal):
    # Dans un vrai problème, on aurait les coordonnées des nœuds
    return 0  # Simplifié pour l'exemple

# Utilisation
chemin = a_star('A', 'D', graph, heuristic)
```

### Avantages de l'approche heuristique

1. **Efficacité** : L'algorithme explore préférentiellement les chemins prometteurs grâce à la heuristique
2. **Optimalité** : Si l'heuristique est admissible (ne surestime jamais la distance), A* garantit de trouver le plus court chemin
3. **Flexibilité** : On peut adapter l'heuristique selon le contexte

## Avantages et inconvénients des algorithmes heuristiques

### Avantages
- Temps d'exécution rapide
- Adaptés aux problèmes complexes
- Peuvent trouver des solutions acceptables rapidement

### Inconvénients
- Ne garantissent pas toujours l'optimalité
- Peuvent tomber dans des optima locaux
- Qualité de la solution dépend de la heuristique choisie

## Applications pratiques

Les algorithmes heuristiques sont largement utilisés dans :
- Planification de routes (GPS)
- Optimisation de réseaux
- Intelligence artificielle
- Jeux vidéo (pathfinding)
- Planification de production