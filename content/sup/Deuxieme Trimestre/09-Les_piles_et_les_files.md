---
title: Les Piles et les Files
weight: 90
---

## Introduction

Les **piles** (stacks) et les **files** (queues) sont des structures de données fondamentales en informatique. Ces structures permettent de stocker et d'organiser des données selon des règles d'accès spécifiques. Elles sont utilisées dans de nombreux algorithmes et applications, des plus simples aux plus complexes.

## Les piles (LIFO - Last In, First Out)

### Principe de fonctionnement

Une pile (stack) est une structure de données de type **LIFO** (Last In, First Out), ce qui signifie que le dernier élément ajouté est le premier à être retiré.

Pensez à une pile d'assiettes :
- On pose les assiettes les unes sur les autres (empiler)
- On ne peut prendre que l'assiette du dessus (dépiler)

### Opérations fondamentales

Une pile possède deux opérations principales :

1. **Empiler (push)** : Ajouter un élément au sommet de la pile
2. **Dépiler (pop)** : Retirer l'élément au sommet de la pile

D'autres opérations courantes incluent :

- **Consulter le sommet (peek/top)** : Voir l'élément au sommet sans le retirer
- **Vérifier si la pile est vide (isEmpty)** : Renvoie vrai si la pile ne contient aucun élément
- **Taille (size)** : Obtenir le nombre d'éléments dans la pile

### Implémentation d'une pile en Python

#### Utilisation d'une liste

```python
class Pile:
    def __init__(self):
        self.elements = []
    
    def est_vide(self):
        return len(self.elements) == 0
    
    def empiler(self, element):
        self.elements.append(element)
    
    def depiler(self):
        if self.est_vide():
            raise Exception("Impossible de dépiler une pile vide")
        return self.elements.pop()
    
    def sommet(self):
        if self.est_vide():
            raise Exception("La pile est vide")
        return self.elements[-1]
    
    def taille(self):
        return len(self.elements)
```

#### Exemple d'utilisation

```python
# Création d'une pile
pile = Pile()

# Empiler des éléments
pile.empiler(5)
pile.empiler(3)
pile.empiler(8)

# Afficher l'état de la pile
print("Taille de la pile :", pile.taille())  # Affiche : 3
print("Élément au sommet :", pile.sommet())  # Affiche : 8

# Dépiler
element = pile.depiler()
print("Élément dépilé :", element)           # Affiche : 8
print("Nouvel élément au sommet :", pile.sommet())  # Affiche : 3

# Dépiler jusqu'à vider la pile
while not pile.est_vide():
    print("Dépilage :", pile.depiler())
```

### Utilisation de la bibliothèque standard Python

Python propose également une implémentation de pile via les collections :

```python
from collections import deque

pile = deque()
pile.append(5)       # Équivalent à empiler
pile.append(3)
pile.append(8)

print(pile[-1])      # Consulter le sommet : 8
element = pile.pop() # Dépiler : 8
```

### Applications courantes des piles

1. **Évaluation d'expressions** : Calcul d'expressions arithmétiques (notation polonaise inversée)
2. **Gestion d'appels de fonctions** : La pile d'appels dans la plupart des langages de programmation
3. **Algorithmes de parcours de graphes** : Parcours en profondeur (DFS)
4. **Vérification de parenthèses** : Déterminer si une expression a des parenthèses bien équilibrées
5. **Annulation d'opérations** : Fonctionnalité "Undo" dans les applications

### Exemple : Vérification de parenthèses

```python
def verifier_parentheses(expression):
    pile = []
    parentheses_ouvrantes = "({["
    parentheses_fermantes = ")}]"
    
    for caractere in expression:
        if caractere in parentheses_ouvrantes:
            pile.append(caractere)
        elif caractere in parentheses_fermantes:
            if not pile:  # Si la pile est vide
                return False
            
            haut = pile.pop()
            # Vérifier que la parenthèse fermante correspond à l'ouvrante
            if parentheses_ouvrantes.index(haut) != parentheses_fermantes.index(caractere):
                return False
    
    # La pile doit être vide à la fin pour que l'expression soit valide
    return len(pile) == 0

# Tests
print(verifier_parentheses("(a + b)"))           # True
print(verifier_parentheses("{[a + b] * (c - d)}")) # True
print(verifier_parentheses("(a + b"))            # False
print(verifier_parentheses("(a + b) * c)"))      # False
print(verifier_parentheses("{[a + b)]"))         # False
```

## Les files (FIFO - First In, First Out)

### Principe de fonctionnement

Une file (queue) est une structure de données de type **FIFO** (First In, First Out), ce qui signifie que le premier élément ajouté est le premier à être retiré.

Pensez à une file d'attente :
- Les personnes se placent à la fin de la file (enfiler)
- La première personne dans la file est la première à être servie (défiler)

### Opérations fondamentales

Une file possède deux opérations principales :

1. **Enfiler (enqueue)** : Ajouter un élément à la fin de la file
2. **Défiler (dequeue)** : Retirer l'élément au début de la file

D'autres opérations courantes incluent :

- **Consulter le premier élément (front)** : Voir le premier élément sans le retirer
- **Vérifier si la file est vide (isEmpty)** : Renvoie vrai si la file ne contient aucun élément
- **Taille (size)** : Obtenir le nombre d'éléments dans la file

### Implémentation d'une file en Python

#### Utilisation d'une liste

```python
class File:
    def __init__(self):
        self.elements = []
    
    def est_vide(self):
        return len(self.elements) == 0
    
    def enfiler(self, element):
        self.elements.append(element)
    
    def defiler(self):
        if self.est_vide():
            raise Exception("Impossible de défiler une file vide")
        return self.elements.pop(0)  # Attention: opération en O(n)
    
    def premier(self):
        if self.est_vide():
            raise Exception("La file est vide")
        return self.elements[0]
    
    def taille(self):
        return len(self.elements)
```

Cette implémentation avec la méthode `pop(0)` n'est pas efficace pour les grandes files car elle nécessite de décaler tous les éléments restants (complexité O(n)).

#### Exemple d'utilisation

```python
# Création d'une file
file = File()

# Enfiler des éléments
file.enfiler(5)
file.enfiler(3)
file.enfiler(8)

# Afficher l'état de la file
print("Taille de la file :", file.taille())   # Affiche : 3
print("Premier élément :", file.premier())    # Affiche : 5

# Défiler
element = file.defiler()
print("Élément défilé :", element)            # Affiche : 5
print("Nouveau premier élément :", file.premier())  # Affiche : 3

# Défiler jusqu'à vider la file
while not file.est_vide():
    print("Défilage :", file.defiler())
```

### Utilisation de la bibliothèque standard Python

Python propose une implémentation efficace de file via les collections :

```python
from collections import deque

file = deque()
file.append(5)        # Enfiler
file.append(3)
file.append(8)

print(file[0])        # Consulter le premier élément : 5
element = file.popleft() # Défiler efficacement : 5
```

L'utilisation de `deque` est recommandée car `popleft()` a une complexité O(1), contrairement à `list.pop(0)` qui est en O(n).

### File à double extrémité (Deque)

Une **deque** (double-ended queue) permet d'ajouter et de retirer des éléments des deux extrémités efficacement :

```python
from collections import deque

d = deque()
d.append(1)      # Ajouter à droite
d.append(2)
d.appendleft(0)  # Ajouter à gauche

print(d)         # deque([0, 1, 2])

d.pop()          # Retirer à droite : 2
d.popleft()      # Retirer à gauche : 0
```

### Applications courantes des files

1. **Gestion de processus** : Ordonnancement des tâches dans les systèmes d'exploitation
2. **Impression** : File d'attente pour les travaux d'impression
3. **Algorithmes de parcours de graphes** : Parcours en largeur (BFS)
4. **Tampons de données** : Communication entre processus/threads
5. **Gestion de services** : Service clients, requêtes web, etc.

## Conclusion

Les piles et les files sont des structures de données fondamentales en informatique, chacune avec ses propres cas d'utilisation.

- Les **piles (LIFO)** sont idéales pour les problèmes où l'ordre inverse est important, comme la gestion des appels de fonctions ou l'exploration en profondeur.
- Les **files (FIFO)** sont parfaites pour les situations où l'ordre chronologique est crucial, comme la gestion des tâches ou l'exploration en largeur.

La maîtrise de ces structures est essentielle pour tout programmeur, car elles servent de base à de nombreux algorithmes et applications plus complexes.

## Ressources supplémentaires

- Documentation Python sur les collections : [https://docs.python.org/fr/3/library/collections.html](https://docs.python.org/fr/3/library/collections.html)
