---
title: Codage
weight: 20
---

## Représentation des données dans la mémoire

Quelle que soit la nature de l'information (image, son, vidéo, texte,
...) traitée par un ordinateur, elle est toujours sous la forme d'un
ensemble de nombres écrits en binaire (0 et 1).

### Système de numération binaire

On appelle base un entier **B** strictement positif. Tout entier **n**
peut alors s'écrire de façon unique comme ci-dessous:
$$ n = \sum_{i = 0}^{k}n_{i}B^{i} = n_{k}B^{k} + n_{k - 1}B^{k - 1} + \ldots + n_{1}B + n_{0} $$
$n$ s'écrit donc:

$$n = \left( n_{k}n_{k - 1} \ldots n_{0} \right)_{B} \text{ avec } n_i \in ⟦0,B⟦ $$ 

On compte habituellement en base 10 mais un ordinateur compte en base 2
car les circuits utilisés peuvent avoir deux états auxquels
correspondent deux chiffres 0 et 1. On parle de numérotation binaire.
Les éléments 0 et 1 sont appelés **BIT** (Binary Digit), Un groupe de
huit bits est nommé **Octet** (**Byte** en anglais.)

Les systèmes informatiques travaillent sur des longueurs fixes de bits
appelées **MOT**. Un MOT est la plus grande série de bits qu'un
ordinateur puisse traiter en une seule opération. Par exemple le
microprocesseur `intel i5` appartient a la famille `x86_64` qui utilise
des mots de 64 bits.

## Représentation des entiers naturels en binaire

Pour obtenir l'expression binaire d'un nombre exprimé en décimal, on
divise le nombre par 2 puis on divise successivement les quotients
obtenus par 2 jusqu'à ce que le quotient final obtenu soit égal à 0. Les
restes obtenus forment la représentation voulu.

#### Exemple:

Pour $n = 77$, on effectue les divisions suivantes:

<figure>
<p><img src="/sup/res/01-divisions.png" style="width:40.0%" /></p>
<figcaption><p>Divisions successives par 2</p></figcaption>
</figure>

La représentation binaire de $77$ est donc $n = (1001101)_{2}$ Avec une
taille de mot de 8 bits, on peut représenter les entiers $⟦0,255⟧$

<br/>

## Représentation des entiers relatifs

### Représentation par signe et valeur absolue sur 8 bits

On représente les nombres positifs comme vu précédemment pour les nombres
naturels sur 7 bits, et on rajoute 0 comme bit de **poids le plus
fort**.\
Pour les nombres négatifs, le bit de poids le plus fort est un 1

#### Exemple:

- $77 = (01001101)_{2}$

- $- 77 = (11001101)_{2}$

**Remarques:**

- Avec une taille de mot de 8 bits, on peut représenter les entiers
  $⟦ - 127,127⟧$

- Le 0 est représenté deux fois: $+0 = (00000000)_2$ et $-0 = (10000000)_2$

### Représentation par Complément à 2 sur 8 bits

On représente les nombres positifs comme vu précédemment pour les nombres
naturels sur 7 bits. On aura donc toujours un 0 comme bit de poids
fort.\
Pour les nombres négatifs, on écrit leur valeur absolue en binaire
naturel, puis on applique la fonction appelée Complément  a 2, qui
consiste a faire le Complément  a 1 puis d'ajouter 1.

#### Exemple:

Pour représenter -77 on commence par la représentation de 77:\
$$77 = (01001101)_2$$ On applique le Complément  a 1 (le NON binaire),
c'est a dire on inverse les 0 en 1 et les 1 en 0. On obtient:
$$(10110010)_2$$ Puis on rajoute 1 et on obtient la représentation de
-77 par Complément  a 2 sur 8 bits : $$- 77 = (10110011)_2$$
**Remarques:**

- Avec une taille de mot de 8 bits, on peut représenter les entiers
  $⟦ - 128,127⟧$

- $C_{2}\left( C_{2}(n) \right) = n$

- $C_{2}(n) + n = 0$

## Représentation des nombres a virgule

### Format virgule fixe

On complete la definition précédente par les puissance de 2 négatives:
$$n = \sum_{i = - k}^{k}n_{i}B^{i} = n_{k}B^{k} + n_{k - 1}B^{k - 1} + \ldots + n_{1}B + n_{0} + n_{- 1}B^{- 1} + \ldots + n_{- k'}B^{- k'}$$

$$n = \left( n_{k} n_{k - 1}\ldots n_{0},n_{- 1}\ldots n_{- k'} \right)\_{B}\quad\text{ avec }\quad n_{i} \in ⟦0,B⟦$$
On représente la partie entière comme pour les entiers naturels. Pour la
partie fractionnaire, on effectue des multiplications successive par
deux, en prenant les parties entières a chaque fois.

#### Exemple:

Pour représenter $13,375$, on représente $13$ par $(1101)\_{2}$, puis on
représente la partie fractionnaire comme suit: $$0,375 \times 2 = 0,75$$
$$0,75 \times 2 = 1,5$$ $$0,5 \times 2 = 1,0$$ On va lire les parties
entières des résultats de haut en bas $(0,011)\_2$\
Donc $$13,375 = (1101,011)_{2}$$

### Format virgule flottante

La norme IEEE 754 définit la manière de représenter les nombres réels a
partir de leur notation scientifique :
$$n = \pm m \times B^{e}\text{ avec }1 \leq m < B$$ En binaire
$1 \leq m < 2$. On note $m'$ la partie fractionnaire de $m$ donc:
$$m = (1,m')\_{2}$$ Ce qui donne : $$n = \pm (1,m')_{2} \times 2^{e}$$ La
norme propose deux format:

- Simple précision qui s’écrit sur 32 bits.

- Double précision, sur 64 bits.

En simple précision le nombre n est représente par trois composantes:

- 1 bit de signe (0 si positif, 1 si négatif)

- 8 bits pour l'exposant modifie: $e' = e + 127$

- 23 bits pour la mantisse (la partie fractionnaire, $m'$)

---

[S]{.box} [e]{.box} [e]{.box} [e]{.box} [e]{.box} [e]{.box} [e]{.box} [e]{.box} [e]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box} [m]{.box}

---

**Remarques:**

- L'exposant 00000000 et l'exposant 11111111 sont interdit.

- On rajoute 127 a l'exposant pour pouvoir représenter les exposants
  de $⟦ - 127,128⟧$

#### Exemple:

Pour coder le nombre $n = 113,25$ :

- n est positif, donc le bit de signe S = 0

$$113 = (01110001)\_{2}\quad\text{ et }\quad 0,25 = (0,01)\_{2}$$ Donc
$$n = (01110001,01)_{2}$$ $$n = 1,11000101 \times 2^{6}$$
$$m' = 11000101\quad\text{ et }\quad e' = 6 + 127 = 133 = (10000101)$$
d'ou la représentation de n : $$0\ 10000101\ 11000101000000000000000$$

# Codage des caractères

L'ASCII est une norme décrivant une table d'encodage sur 7 bits de 128
caractères pour les systèmes informatiques. Elle est apparue dans les
années 1960 et est notamment utilisée pour le codage des 95 caractères
imprimables d'une machine à écrire

L'ASCII définit 128 caractères numérotés de 0 à 127 et codés en binaire
de 0000000 à 1111111. Sept bits suffisent donc. Toutefois, les
ordinateurs travaillant presque tous sur un multiple de huit bits (un
octet) depuis les années 1970, chaque caractère d'un texte en ASCII est
souvent stocké dans un octet dont le 8e bit est 0.

<figure>
<p><img src="/sup/res/01-ASCII.png" style="width:90.0%" /></p>
<figcaption><p>Tableau ASCII</p></figcaption>
</figure>
