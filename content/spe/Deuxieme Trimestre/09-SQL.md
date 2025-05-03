---
title: SQL
weight: 90
---

## Introduction aux bases de données relationnelles

Les bases de données SQL suivent le modèle **relationnel**, qui permet d'organiser les données dans plusieurs **tables** composées de colonnes. Ce modèle offre plusieurs avantages :
- Intégrité des données
- Cohérence
- Facilité de maintenance
- Performance des requêtes

## Concepts fondamentaux

### Tables et relations
- Une **table** est une structure qui contient des données organisées en colonnes
- Chaque ligne d'une table représente un enregistrement
- Les **relations** entre les tables sont établies via des clés étrangères

### Types de données courants
- `INTEGER` : nombres entiers
- `REAL` : nombres décimaux
- `TEXT` : chaînes de caractères
- `DATE` : dates
- `BOOLEAN` : valeurs vrai/faux

## Commandes SQL de base

### Création de tables
```sql
CREATE TABLE Etudiants (
    id INTEGER PRIMARY KEY,
    nom TEXT NOT NULL,
    prenom TEXT NOT NULL,
    age INTEGER,
    classe TEXT
);
```

### Insertion de données
```sql
INSERT INTO Etudiants (id, nom, prenom, age, classe)
VALUES (1, 'Dupont', 'Jean', 18, 'MPSI1');
```

### Requêtes simples
```sql
-- Sélectionner toutes les colonnes
SELECT * FROM Etudiants;

-- Sélectionner des colonnes spécifiques
SELECT nom, prenom FROM Etudiants;

-- Filtrer avec WHERE
SELECT * FROM Etudiants WHERE age > 18;

-- Trier avec ORDER BY
SELECT * FROM Etudiants ORDER BY nom;
```

## Requêtes avancées

### Jointures
```sql
-- Jointure interne
SELECT e.nom, e.prenom, n.note
FROM Etudiants e
JOIN Notes n ON e.id = n.etudiant_id;

-- Jointure externe
SELECT e.nom, e.prenom, n.note
FROM Etudiants e
LEFT JOIN Notes n ON e.id = n.etudiant_id;
```

### Agrégation
```sql
-- Moyenne par classe
SELECT classe, AVG(age) as moyenne_age
FROM Etudiants
GROUP BY classe;

-- Compter le nombre d'étudiants
SELECT COUNT(*) as total_etudiants
FROM Etudiants;
```

### Sous-requêtes
```sql
-- Trouver les étudiants plus âgés que la moyenne
SELECT nom, prenom, age
FROM Etudiants
WHERE age > (SELECT AVG(age) FROM Etudiants);
```
## Applications pratiques

Les bases de données SQL sont utilisées dans :
- Gestion des stocks
- Systèmes de réservation
- Sites web dynamiques
- Applications mobiles
- Systèmes de gestion d'entreprise

