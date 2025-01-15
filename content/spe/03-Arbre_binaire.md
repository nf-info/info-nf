---
title: Arbres binaires
weight: 30
---

## Définitions

**En mathématique:** Un arbre est un cas spécial de graphe acyclique
oriente, ou tous les nœuds sauf la racine ont un unique parent

**En informatique:** C'est une structure de données récursive utilisée
pour représenter ce type de graphes.

## Exemples et terminologie

<figure>
<p><img src="../res/03-arbre_1.png" style="width:60.0%" /></p>
<figcaption><p>Un arbre contenant des entiers</p></figcaption>
</figure>

Un arbre est un ensemble de **nœuds** et d'**arête** reliant ces
nœudsChaque nœud a une **étiquette** : une valeur ou donnée associée au
nœud.\
**L'ordre** ou la **taille** d'un arbre est le nombre de nœuds qui le
compose.\
La **racine** d'un arbre est le nœud le plus haut dans l’hiérarchie de
l'arbre, c'est le nœud "de départ".\
Tous les nœuds sauf la racine ont un unique **père**, c'est le nœud
directement au-dessus dans l’hiérarchie.\
Les nœuds ont 0, 1, ou plusieurs **fils**. Les nœuds sans fils sont
appelé **feuilles** de l'arbre.\
Le **degré** d'un nœud est le nombre de fils qu'il a.\
La **profondeur** d'un nœud est le nombre d’arête nécessaire pour aller
du nœud a la racine.\
On s’intéresse dans ce cours aux arbres **binaires**, c-a-d, les arbres
ayant des nœuds de degré maximum 2.\

<figure>
<p><img src="../res/03-arbre_2.png" style="width:60.0%" /></p>
<figcaption><p>Classe de complexité</p></figcaption>
</figure>

## Structure récursive

On peut définir les arbres binaires de manière récursive. Un arbre est :

- Soit vide, représenté par une liste vide `[]`.

- Soit compose d'un nœud racine ayant une valeur $V_{r}$, d'un
  sous-arbre gauche $F_{g}$, et d'un sous-arbre droit $F_{d}$. On
  représente l'arbre par la liste `[V_r, F_g, F_d]`.

#### Exemples

- `[2, [], []]`

- `[4, [2, [], []], [8, [1, [], []], []] ]`

- `[7, [3, [1, [], []], [2, [], []]], [5, [4, [], []], []] ]`

## Implémentation

```py
def crée_arbre():
    return []
def arbre(R, Fg, Fd):
    return [R, Fg, Fd]
def est_vide(A):
    return A == []
def fils_g(A):
    if est_vide(A): return None
    return A[1]
def fils_d(A):
    if est_vide(A): return None
    return A[2]
def racine(A):
    if est_vide(A): return None
    return A[0]
def est_arbre(A):
    return est_vide(A) or (isinstance(A, list) and len(A) ==3 and est_arbre(fils_g(A)) and est_arbre(fils_d(A))
def est_feuille(A):
    return not est_vide(A) and est_vide(fils_g(A)) and est_vide(fils_d(A))
```

## Parcours

On peut parcourir l'arbre en privilégiant la largeur, ou la profondeur.

### Parcours en profondeur (Depth-First Search):

#### Préfixe :

On parcourt l'arbre récursivement suivant l'ordre : $V_{r},F_{g},F_{d}$

#### Infixe :

On parcourt l'arbre récursivement suivant l'ordre : $F_{g},V_{r},F_{d}$

#### Postfix :

On parcourt l'arbre récursivement suivant l'ordre : $F_{g},F_{d},V_{r}$

### Parcours en largeur (Breadth-First Search)

On liste tous les fils du même niveau de profondeur avant de passer au
niveau de profondeur suivant.

#### Implémentation

```py
def parcours_préfixe(A):
    if est_vide(A) :
        return []
    return [racine(A)] + parcours_préfixe(fils_g(A)) + \
             parcours_préfixe(fils_d(A))
def parcours_infixe(A):
    if est_vide(A) :
        return []
    return parcours_infixe(fils_g(A)) + [racine(A)] + \
             parcours_infixe(fils_d(A))
def parcours_postfix(A):
    if est_vide(A) :
        return []
    return parcours_postfix(fils_g(A)) + parcours_postfix(fils_d(A)) + \
            [racine(A)]

def BFS(A):
    F = [A]
    while F!=[]:
        x = F.pop(0)

        # Traitement sur x
        print(racine(x))

        # Ajout des fils dans la file
        if not est_vide(fils_g(A)):
            F.append(fils_g(x))
        if not est_vide(fils_d(A)):
            F.append(fils_d(x))
```

# Arbre Binaire de Recherche (Binary Search Tree)

Un ABR `A` est un arbre binaire qui vérifie les conditions suivantes :

- Les étiquettes du sous-arbre gauche sont inférieures a celle de la
  racine

- Les étiquettes du sous-arbre droit sont supérieures a celle de la
  racine

- Les sous-arbres gauche et droit sont des ABR (récursivité)

<figure>
<p><img src="../res/03-ABR.png" style="width:90.0%" /></p>
<figcaption><p>Un ABR</p></figcaption>
</figure>

On peut obtenir les étiquettes d'un ABR en ordre croissant en faisant un
parcours infixe.

## Implémentation

```py
def min_abr(ABR):
    current = ABR
    while not est_vide(fils_g(current)):
        current = fils_g(current)
    return racine(current)
def max_abr(ABR):
    current = ABR
    while not est_vide(fils_d(current)):
        current = fils_d(current)
    return racine(current)
def insert(ABR, e):
    if est_vide(ABR):
        ABR = [e, [], []]
    elif e <= racine(ABR) :
        insert(fils_g(ABR), e)
    else :
        insert(fils_d(ABR), e)

def search(ABR, e):
    if est_vide(ABR) :
        return False
    if racine(ABR) == e:
        return True
    if e < racine(ABR) :
        return search(fils_g(ABR), e)
    if e > racine(ABR) :
        return search(fils_d(ABR), e)

def prédécesseur(ABR, e):
    if est_vide(fils_g(ABR)) :
        return None
    return max_abr(fils_g(ABR))
def successeur(ABR, e):
    if est_vide(fils_d(ABR)) :
        return None
    return min_abr(fils_d(ABR))
def remove(ABR, e):
    # ...

```

# Tas

Un Tas `T` est un arbre binaire qui vérifie les conditions suivantes :

- Il est **parfait**, c'est a dire tous les niveaux sauf le dernier
  doivent être totalement remplis et le dernier niveau est rempli de
  gauche à droite.

- l’étiquette de chaque nœud est supérieure ou égale (resp.
  inférieure ou égale) aux étiquettes de ses fils, on parle de tas
  **max** (resp. tas **min**)

<figure>
<p><img src="../res/03-tas.png" style="width:60.0%" /></p>
<figcaption><p>Un tas</p></figcaption>
</figure>

## Implémentation

Le tas étant un arbre binaire parfait, on peut l’implémenter en
utilisant une seule liste, ou on met la racine a l'indice 0, et pour
chaque nœud `i` on met les fils gauche et droit aux position `2*i+1` et
`2*i+2`.

Le tas précédent est donc implémente comme suit :
`T = [53, 41, 30, 36, 28, 21, 6, 31, 16, 20]`

```py
def crée_tas():
  return []
def insert(T, e):
  # ...
def enlève_racine(T):
  # ...
```

## Tri par tas (Heap sort)

On peut utiliser les tas pour faire le tri: Pour une liste `L`, on
insère successivement les elements de `L` dans un tas min, puis on
enlève la racine successivement jusqu'a vider le tas, la racine étant le
min a chaque itération, l'ordre des racine enlève sera donc croissant.

```py
def tri_par_tas(L):
    # ...
```
