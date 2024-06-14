# LMD : Langage de Manipulation de Données (DML: Data Manipulation Langage)

### Insérer des données (CREATE)
```sql
INSERT INTO movie (nom,date_sortie) VALUES ('Pulp Fiction', '2001-10-23'), ('The Revenant', '2015-04-30');
```

```sql
INSERT INTO director (nom, prenom) VALUES ('Spike', 'Lee'),('Steven','Spielbierg'),('Chritopher', 'Nolan'),('Luc', 'Besson');
```

```sql
INSERT INTO director (nom, prenom, age, email,birth,salaire, pays_origine) VALUES ('Duvernay', 'Ava', 40, 'AvaDuv@gmail.com', '1980-12-04', 200000.600,'AG'),('Mcqueen', 'Steve', 60, 'McqueenSteevie@gmail.com', '1960-12-04', 100000,'SD'), ('Coogler', 'Ryan', 30, 'Coocoo@gmail.com', '1994-12-04',850000,'ML'),('Singleton', 'John', 25, 'JohnnySgl@gmail.com', '1998-12-04',900000,'FR');
```

### Afficher des données (READ)

```sql
SELECT * FROM director;

SELECT * FROM director WHERE age= 19 AND pays='FR';

SELECT * FROM director WHERE age BETWEEN 40 AND 60;

SELECT * FROM director WHERE nom LIKE '%an';

SELECT * FROM movie WHERE prenom IN ('Lee', 'Stan');

```
### EXERCICE 1

```sql
<!-- Afficher le prenom et l'email des réalisateur dont le nom contient un 'e' et où le pays est FR ou UK et age est supérieur à 3O ans -->

SELECT prenom, email FROM director WHERE nom LIKE '%e%' AND (pays_origine ='FR' OR pays_origine ='AG') AND age > 30;

SELECT prenom, email FROM director WHERE nom LIKE '%e%' AND pays_origine IN ('FR', 'UK') AND age > 30;

SELECT prenom, email FROM director WHERE nom LIKE '%e%' AND pays_origine IN ('FR', 'UK') AND age > 30 ORDER BY email DESC;
```

### Mettre à jour les données (UPDATE)

````sql
UPDATE director SET nom='test';

-- Tous les pays seront sur 'FR' pour les id de 0 à 10

UPDATE director SET pays_origine='fr' WHERE id<=10;

-- Mettre le salaire à 1 000 000 pour les director qui ont moins de 20 ans ou entre 40 et 60 ans

UPDATE director SET salaire = 1000000000 WHERE age<=20 OR age BETWEEN 40 AND 60;

-- Mettre à jour la colonne salaire pour pouvoir avoir 12 chiffre dont 2 après la virgule.

ALTER TABLE director
MODIFY  salaire DECIMAL (14,2);
````
### Supprimer des données (DELETE)

````sql
DELETE  FROM director;
-- Supprimer les realisateurs qui n'ont pas la valeur FR ou UK en pays_origine.

DELETE FROM director WHERE pays_origine NOT IN ('FR', 'UK');
````


