# Exercice avec une Base de Données pour une École

Dans cet exercice, nous allons créer une base de données pour gérer des étudiants, des matières et des notes dans une école.

### 1. Créez la Base de Données `school_db`

```sql
CREATE DATABASE school_db;
```

### 2. Utilisez la Base de Données

```sql
USE school_db;
```

### 3. Créer la table "student" avec id, nom, prenom, date_naissance, adresse, email

```sql
CREATE TABLE student (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(50),
    prenom VARCHAR(50),
    date_naissance DATE,
    adresse VARCHAR(100),
    email VARCHAR(100)
);
```

### 4. Créer la table "subject" id, nom, description

```sql
CREATE TABLE subject (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(50),
    description VARCHAR(100)
);
```

### 5. Créer la table "note" avec un id note et des clés étrangères pour student_id et subject_id

```sql
CREATE TABLE note (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    matiere_id INT,
    note FLOAT,
    FOREIGN KEY (student_id) REFERENCES student(id),
    FOREIGN KEY (matiere_id) REFERENCES subject(id)
);
```

### 6. Insérez des Données dans les Tables

#### a. Insertion des Étudiants

```sql
INSERT INTO student (nom, prenom, date_naissance, adresse, email)
VALUES
('Doe', 'John', '2000-01-01', '123 Main Street', 'john.doe@example.com'),
('Smith', 'Emma', '1999-03-15', '456 Elm Street', 'emma.smith@example.com'),
('Johnson', 'Michael', '2001-05-10', '789 Oak Street', 'michael.johnson@example.com'),
('Brown', 'Olivia', '2002-07-20', '321 Pine Street', 'olivia.brown@example.com'),
('Taylor', 'Sophia', '2003-09-25', '654 Maple Street', 'sophia.taylor@example.com'),
('Anderson', 'Liam', '2000-12-05', '987 Cedar Street', 'liam.anderson@example.com'),
('Clark', 'Ava', '1998-02-14', '741 Birch Street', 'ava.clark@example.com'),
('Lewis', 'Noah', '1999-04-30', '852 Walnut Street', 'noah.lewis@example.com'),
('Walker', 'Mia', '2001-06-08', '369 Oakwood Street', 'mia.walker@example.com'),
('Hall', 'Elijah', '2002-08-16', '258 Cherry Street', 'elijah.hall@example.com');
```

#### b. Insertion des Matières

```sql
INSERT INTO subject (nom, description)
VALUES
('Mathématiques', 'Calcul et algèbre'),
('Sciences', 'Physique et chimie'),
('Histoire', 'Événements historiques'),
('Français', 'Grammaire et littérature'),
('Anglais', 'Conversation et grammaire');
```

#### c. Insertion des Notes

```sql
INSERT INTO note (student_id, matiere_id, note)
VALUES
(1, 1, 15.5),
(1, 2, 12.0),
(2, 3, 14.5),
(2, 4, 16.0),
(3, 5, 13.5),
(3, 1, 17.0),
(4, 2, 13.0),
(4, 3, 11.5),
(5, 4, 18.0),
(5, 5, 16.5);
```

---

## Voici quelques exemples de requêtes SQL avec des conditions, des limites et du tri appliqués à la table "étudiant" :

### 1. Sélectionner tous les étudiants dont le nom est "Doe" :

```sql
SELECT *
FROM student
WHERE nom = 'Doe';
```

### 2. Sélectionner tous les étudiants âgés de moins de 20 ans :


```sql
SELECT *
FROM student
WHERE date_naissance > DATE_SUB(CURDATE(), INTERVAL 20 YEAR);
```

### 3. Sélectionner les 5 premiers étudiants dans l'ordre alphabétique des noms :

```sql
SELECT *
FROM student
ORDER BY nom
LIMIT 5;
```

### 4.Sélectionner les étudiants par ordre décroissant de leur date de naissance :

```sql
SELECT *
FROM student
ORDER BY date_naissance DESC;
```

### 5. Sélectionner les étudiants dont l'adresse contient le mot "Street" et limiter les résultats à 3 :


```sql
SELECT *FROM student WHERE adresse LIKE '%Street%' LIMIT 3;
```

### 6. Sélectionner les étudiants dont le nom commence par "S" et trier les résultats par prénom :


```sql
SELECT * FROM student WHERE nom LIKE 'S%' ORDER BY prenom;
```

Ces exemples montrent comment appliquer des conditions, des limites et du tri dans vos requêtes SQL pour la table "student". N'hésitez pas à les ajuster en fonction de vos critères de recherche spécifiques.
---
### Voici quelques exemples de requêtes SQL qui utilisent les fonctions MIN, MAX, COUNT, GROUP BY et HAVING :

### 1. Sélectionner la note minimale, maximale et le nombre total de notes pour chaque matière :

```sql
SELECT subject.nom AS matieres, MIN(note) AS note_minimale, MAX(note) AS note_maximale, COUNT(*) AS nombre_notes FROM note INNER JOIN subject ON subject.id = subject_id GROUP BY subject_id;


```

### 2. Sélectionner les étudiants ayant une moyenne supérieure à 15 :


```sql
SELECT student_id, 
rt(note) AS moyenne
FROM note
GROUP BY student_id
HAVING AVG(note) > 15;
```

### 3. Sélectionner le nombre d'étudiants ayant obtenu une note supérieure à 16 dans chaque matière :

```sql
SELECT subject_id, COUNT(*) AS nombre_etudiants
FROM note
WHERE note > 16
GROUP BY subject_id;
```

### 4. Sélectionner les matières ayant au moins cinq étudiants :

```sql
SELECT subject_id, COUNT(*) AS nombre_etudiants
FROM note
GROUP BY subject_id
HAVING COUNT(*) >= 5;
```

### 5. Sélectionner les étudiants ayant obtenu une note maximale dans chaque matière :

```sql
SELECT subject_id, student_id, MAX(note) AS note_maximale
FROM note
GROUP BY subject_id;
```
Ces exemples illustrent l'utilisation des fonctions MIN, MAX, COUNT, GROUP BY et HAVING pour effectuer des calculs et filtrer les données en fonction de certaines conditions.
N'hésitez pas à les adapter en fonction de votre base de données et de vos besoins spécifiques.
---

<!-- ! ATTENTION C est aussi une requete! -->

Cette requête sélectionne les noms d'étudiants dont la date de naissance est postérieure au 1er janvier 2000, groupe les résultats par nom, filtre les groupes ayant plus de 2 étudiants, trie les résultats par nom et limite les résultats à 10.
ùlp