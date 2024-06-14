### EXERCICE BANDE DESSINEES

<!--  Voici un exemple d'exercice avec une base de données pour des bandes dessinées belges, en incluant plusieurs tables telles que "BD", "auteur" et "editeur" :   -->

````sql

-- 1. Créez une base de données bd_collection_db:

CREATE DATABASE bd_collection_db;

-- 2. Sélectionnez la base de données nouvellement créée :

USE bd_collection_db ;

--  3. Créez la table "auteur" avec des colonnes telles que "id" (clé primaire), "name" et "nationality" :

CREATE TABLE auteur (
      id INT PRIMARY KEY  AUTO_INCREMENT,
      name VARCHAR(255),
     nationality VARCHAR(255)   
);

-- 4. Insérez des données dans la table "auteur" pour représenter les auteur des bandes dessinées :

INSERT INTO auteur (name, nationality)
   VALUES ('Hergé', 'Belge'), ('René Goscinny', 'Français'), ('Albert Uderzo', 'Français');


-- 5. Créez la table "editeur" avec des colonnes telles que "id" (clé primaire), "nom" et "pays" :

CREATE TABLE editeur (
      id INT PRIMARY KEY  AUTO_INCREMENT,
      name VARCHAR(255),
    pays VARCHAR(255)   
);


-- 6. Insérez des données dans la table "editeur" pour représenter les éditeurs des bandes dessinées :


INSERT INTO editeur (name, pays)
   VALUES ('Casterman', 'Belgique'),('Dargaud', 'France'),('Dupuis', 'Belgique');


-- 7. Créez la table "bd" avec des colonnes telles que "id" (clé primaire), "titre", "auteur_id" (clé étrangère faisant référence à la table auteur), "editeur_id" (clé étrangère faisant référence à la table editeur) et "année_parution" :

CREATE TABLE bd (
      id INT PRIMARY KEY  AUTO_INCREMENT, 
      titre VARCHAR (255),
      auteur_id INT,
      editeur_id INT,
     annee_parution YEAR,
     FOREIGN KEY (auteur_id) REFERENCES auteur(id),
      FOREIGN KEY (editeur_id) REFERENCES editeur(id)
);


-- 8. Insérez des données dans la table "bd" pour représenter différentes bandes dessinées avec leurs auteur et éditeurs :

--     ('Tintin au Tibet', 1, 1, 1960),
--     ('Astérix le Gaulois', 2, 2, 1961),
--     ('Les Aventures de Blake et Mortimer', 1, 3, 1946);


INSERT INTO bd (titre, auteur_id, editeur_id,annee_parution)
   VALUES ('Tintin au Tibet', 7, 1, 1960),('Astérix le Gaulois', 8, 2, 1961),
('Les Aventures de Blake et Mortimer', 9, 3, 1946);


9. Effectuez des requêtes pour afficher les informations sur les bandes dessinées, les auteur et les éditeurs :

    - Afficher toutes les bandes dessinées avec les informations complètes :

SELECT * FROM bd;
    
select* from bd inner join auteur on auteur.id=auteur_id inner join editeur on editeur.id=editeur_id;

    - Afficher les bandes dessinées publiées par un éditeur spécifique (par exemple, "Casterman") :
    
SELECT * FROM bd INNER JOIN editeur ON editeur.id=editeur_id WHERE editeur.name = 'Casterman';

    - Afficher les bandes dessinées publiées après une certaine année (par exemple, après 1960) :


SELECT * FROM bd WHERE annee_parution>1960;




````
Cet exercice vous permet de créer une base de données pour des bandes dessinées belges, de gérer les relations entre les tables "bd", "auteur" et "editeur", et d'effectuer des requêtes pour obtenir des informations spécifiques.
Vous pouvez ajouter davantage de données, de tables et d'autres fonctionnalités de MySQL pour enrichir votre base de données selon vos besoins.

