---
title: Correction et Terminaison des Algorithmes
weight: 80
---
La correction et la terminaison sont deux propriétés fondamentales pour évaluer la qualité d'un algorithme. Un algorithme efficace doit non seulement produire le résultat attendu (correction), mais aussi s'arrêter après un nombre fini d'étapes (terminaison).

## La Correction d'un Algorithme

La correction d'un algorithme désigne sa capacité à produire le résultat attendu pour toutes les entrées valides.

### Types de Correction

- **Correction partielle** : L'algorithme produit le résultat correct *s'il termine*. Cela signifie que si l'algorithme s'arrête, alors son résultat est correct.
  
- **Correction totale** : L'algorithme produit le résultat correct *et* termine son exécution en un temps fini. Une correction totale implique donc à la fois la correction partielle et la terminaison.

### Méthodes de Preuve de Correction

#### Preuve directe

On démontre que pour toute entrée valide, l'algorithme produit bien la sortie attendue.

**Exemple** : Preuve de correction de l'algorithme de recherche linéaire

```python
def recherche_lineaire(liste, element):
    for i in range(len(liste)):
        if liste[i] == element:
            return i
    return -1
```

Pour prouver sa correction, on examine deux cas :
1. Si l'élément est présent dans la liste, l'algorithme retourne l'indice de sa première occurrence.
2. Si l'élément n'est pas dans la liste, l'algorithme retourne -1.

#### Invariants de boucle

Un invariant de boucle est une propriété qui reste vraie avant et après chaque itération d'une boucle.

**Méthode de preuve** :
1. **Initialisation** : Prouver que l'invariant est vrai avant la première itération.
2. **Conservation** : Prouver que si l'invariant est vrai avant une itération, il reste vrai après.
3. **Terminaison** : Prouver que lorsque la boucle se termine, l'invariant combiné avec la condition de sortie permet d'établir la correction de l'algorithme.

**Exemple** : Preuve de correction de l'algorithme de tri par insertion

```python
def tri_insertion(L):
    for i in range(1, len(L)):
        cle = L[i]
        j = i - 1
        while j >= 0 and L[j] > cle:
            L[j + 1] = L[j]
            j -= 1
        L[j + 1] = cle
```

**Invariant** : À chaque début d'itération de la boucle externe, le sous-tableau A[0..i-1] est trié.

- **Initialisation** : Avant la première itération, i=1 et le sous-tableau A[0..0] ne contient qu'un seul élément, donc il est trivialement trié.
- **Conservation** : Supposons que A[0..i-1] est trié avant une itération. Après l'itération, l'élément A[i] est inséré à sa position correcte dans le sous-tableau, maintenant A[0..i] est trié.
- **Terminaison** : À la fin, i=n et A[0..n-1] (le tableau entier) est trié.

## La Terminaison d'un Algorithme

La terminaison garantit que l'algorithme s'arrête après un nombre fini d'étapes. Pour prouver la terminaison, il faut généralement montrer qu'une certaine quantité (appelée "variant") décroît strictement à chaque itération et ne peut pas décroître indéfiniment.

### Variants de boucle

Un variant de boucle est une quantité qui :
1. Est toujours positive ou nulle
2. Décroît strictement à chaque itération
3. A une borne inférieure (généralement 0)

**Exemple** : Preuve de terminaison de l'algorithme d'Euclide pour le PGCD

```python
def pgcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
```

**Variant** : La valeur de b

- **Positivité** : b est toujours positif ou nul par définition.
- **Décroissance** : À chaque itération, b devient a % b, qui est strictement inférieur à b.
- **Borne inférieure** : b ne peut pas être négatif, donc 0 est une borne inférieure.

Puisque b décroît strictement et est borné par 0, l'algorithme terminera nécessairement.

### Terminaison des Algorithmes Récursifs

Pour les algorithmes récursifs, la terminaison est prouvée en montrant que chaque appel récursif se rapproche d'un cas de base et que ce cas sera atteint en un nombre fini d'appels.

**Exemple** : Preuve de terminaison de l'algorithme de factorielle

```python
def factorielle(n):
    if n <= 1:
        return 1
    return n * factorielle(n-1)
```

**Variant** : La valeur de n

- À chaque appel récursif, n diminue de 1
- Le cas de base est atteint lorsque n ≤ 1
- Si n est un entier naturel, le cas de base sera atteint en au plus n appels récursifs

## Correction des Programmes Récursifs

La preuve de correction des programmes récursifs utilise souvent le principe de récurrence.

### Méthode de preuve par récurrence

1. **Cas de base** : Montrer que l'algorithme est correct pour les entrées les plus simples.
2. **Hypothèse de récurrence** : Supposer que l'algorithme est correct pour toutes les entrées de taille inférieure à n.
3. **Pas de récurrence** : Montrer que l'algorithme est correct pour une entrée de taille n en utilisant l'hypothèse de récurrence.

**Exemple** : Preuve de correction de l'algorithme de factorielle

```python
def factorielle(n):
    if n <= 1:
        return 1
    return n * factorielle(n-1)
```

1. **Cas de base** : Pour n ≤ 1, l'algorithme retourne correctement 1 = 1!
2. **Hypothèse de récurrence** : Supposons que factorielle(k) calcule correctement k! pour tout k < n.
3. **Pas de récurrence** : Pour n, l'algorithme calcule n * factorielle(n-1). Par hypothèse de récurrence, factorielle(n-1) = (n-1)!, donc l'algorithme retourne n * (n-1)! = n!, ce qui est correct.

## Importance de la Correction et de la Terminaison

Un algorithme qui n'est pas correct peut produire des résultats erronés, tandis qu'un algorithme qui ne termine pas consommera des ressources indéfiniment sans fournir de résultat. Ces deux propriétés sont donc essentielles :

- La **correction** assure la fiabilité des résultats
- La **terminaison** garantit l'obtention d'un résultat en temps fini

Dans certains contextes spécifiques, des algorithmes qui ne terminent pas (comme les systèmes d'exploitation ou les serveurs) sont conçus intentionnellement pour fonctionner indéfiniment, mais ils doivent tout de même répondre correctement à chaque requête individuelle.

## Conclusion

La correction et la terminaison sont des propriétés fondamentales que tout algorithme doit satisfaire pour être considéré comme valide. Les preuves formelles de ces propriétés sont essentielles dans les applications critiques où la moindre erreur peut avoir des conséquences graves. Les techniques comme les invariants de boucle, les variants et les preuves par récurrence sont des outils puissants pour établir ces propriétés.