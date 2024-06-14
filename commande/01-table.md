# LDD : Langage de Définitions de Données (DDL: Data Definition Language)

### Affichage des tables :
```sql
SHOW TABLES;
```

### Création d'une table :
```sql
CREATE TABLE film (
id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
nom VARCHAR(255),
date_sortie DATE DEFAULT '2000-01-01'
);
```

### Afficher la structure d'une table :
```sql
DESCRIBE nom_table;
```


### Afficher le create table :
```sql
SHOW CREATE TABLE nom_table;
```

<!-- créer une table realisateur -->
<!-- id -->
<!-- nom (obligé) -->
<!-- prenom (obligé) -->
<!-- âge (vérifier que âge > 18) -->
<!-- email (mais unique) -->
<!-- date de naissance par défaut date du jour-->
<!-- salaire qui peut être un nombre à virgule -->


### EXERCICE 1
```SQL
CREATE TABLE realisateur (
    id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR(255) NOT NULL,
    prenom VARCHAR(255) NOT NULL,
    age TINYINT UNSIGNED CHECK (age>=18),
    email VARCHAR (255) UNIQUE,
    birth DATE DEFAULT CURDATE(),
    salaire DECIMAL (12,2)
);
```
### EXERCICE 2
<!-- On s'est trompé !!!! =( -->
```Sql
<!-- Rennomer la table realisateur en director -->

RENAME TABLE realisateur TO director;

<!-- Renommer la table film en 'Movie' -->

RENAME TABLE film TO movie;

<!-- Modifier la table director pour ajouter la colonne pays d'origine =>'FR' -->

ALTER TABLE director 
ADD pays_origine CHAR (2);

<!-- Modifier la colonne salaire pour que le type soit DECIMAL (8,2) -->

ALTER TABLE director
MODIFY  salaire DECIMAL (8,2);

<!-- Modifier la table movie pour rajouter la contrainte 'unique' sur le nom du film -->

ALTER TABLE movie 
ADD CONSTRAINT UNIQUE (nom);

<!-- Créer une table test avec un id -->

CREATE TABLE  test(
    id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
);

<!-- Supprimer la table test -->
DROP TABLE test;

<!-- Renommer colonne -->
ALTER TABLE director CHANGE salaire salary DECIMAL (10,2);

<!-- Enlever une contrainte -->
ALTER TABLE movie DROP INDEX nom;

```

<!-- Ajouter une colonne id_director dans la table movie -->
```sql
ALTER TABLE movie ADD id_director INT;

ALTER TABLE movie MODIFY id_director INT UNSIGNED;

ALTER TABLE movie ADD CONSTRAINT fk_id_director FOREIGN KEY (id_director)
REFERENCES director (id);
```