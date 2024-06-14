### EXERCICE

````sql

<!-- Exercice avec une base de données pour des figurine Avengers :

1. Créez une base de données avec le nom avengers_db :

CREATE DATABASE avengers_db;

2.Sélectionnez la base de données nouvellement créée :
USE avengers_db;


3.Créez la table "figurine" avec des colonnes telles 

CREATE TABLE figurine (
      id INT UNSIGNED PRIMARY KEY  AUTO_INCREMENT,
      nom VARCHAR(255),
      super_pouvoir VARCHAR(255), 
      annee_sortie YEAR,
      description VARCHAR (255) (text)
);

que "id" (clé primaire), "nom", "super_pouvoir", "annee_sortie" et "description" :
Insérez des données dans la table "figurine" pour représenter des figurine Avengers :
('Iron Man', 'Armure surpuissante', 2008, 'Milliardaire et génie inventeur.'),
('Captain America', 'Force et endurance surhumaines', 2011, 'Héros emblématique de la Seconde Guerre mondiale.'),
('Thor', 'Contrôle de la foudre et marteau magique', 2011, 'Dieu nordique du tonnerre et prince d'Asgard.'),
('Hulk', 'Force et résistance surhumaines', 2008, 'Scientifique transformé en monstre vert lorsqu'il est en colère.'),
('Black Widow', 'Expert en arts martiaux et espionnage', 2010, 'Agent secret russe doté de grandes compétences.'),
('Black Panther', 'Force, vitesse et agilité surhumaines', 2018, 'Roi du Wakanda et protecteur de son peuple.');

 INSERT INTO figurine (nom, super_pouvoir, annee_sortie, description)
   VALUES ('Iron Man', 'Armure surpuissante', 2008, 'Milliardaire et génie inventeur.'),
('Captain America', 'Force et endurance surhumaines', 2011, 'Héros emblématique de la Seconde Guerre mondiale.'),
('Thor', 'Contrôle de la foudre et marteau magique', 2011, 'Dieu nordique du tonnerre et prince d_Asgard.'),
('Hulk', 'Force et résistance surhumaines', 2008, 'Scientifique transformé en monstre vert lorsqu_il est en colère.'),
('Black Widow', 'Expert en arts martiaux et espionnage', 2010, 'Agent secret russe doté de grandes compétences.'),
('Black Panther', 'Force, vitesse et agilité surhumaines', 2018, 'Roi du Wakanda et protecteur de son peuple.');



Effectuez des requêtes pour afficher les figurine Avengers :
4.Afficher toutes les figurine :
SELECT * FROM figurine;

Afficher les figurine sorties après 2010 : 

SELECT * FROM figurine WHERE annee_sortie>2010;

Afficher les figurine avec le pouvoir "Force" dans leur super_pouvoir :

SELECT * FROM figurine WHERE super_pouvoir LIKE '%Force%';


Modifiez une figurine dans la table "figurine" :
Modifiez la description de "Black Panther" pour "Prince de Wakanda et protecteur de son peuple."

UPDATE figurine SET description = 'Prince de Wakanda et protecteur de son peuple.' WHERE nom = 'Black Panther';


Supprimez la figurine Black Widow de la table "figurine" :

DELETE FROM figurine WHERE nom = 'Black Widow';
 -->

Créer la table "weapon" avec des colonnes telles que "id" (clé primaire), "nom", "description" :

CREATE TABLE weapon(
      id INT UNSIGNED PRIMARY KEY  AUTO_INCREMENT,
      nom VARCHAR(255),
      description TEXT
);


Insérez des données dans la table "weapon" pour représenter des armes Avengers :

INSERT INTO weapon (nom, description)
   VALUES('Marteau', 'Marteau magique de Thor.'),
    ('Bouclier', 'Bouclier indestructible.'),
    ('Arc et flèches', 'Arc et flèches de Hawkeye.'),
    ('Armure', 'Armure spéciale conçue pour combattre Hulk.'),
    ('Vibranium Claws', 'Griffes en vibranium indestructible .');

Modifier la table "figurine" pour ajouter une colonne "weapon_id" :
ALTER TABLE figurine ADD COLUMN weapon_id INT;

Modifier la table "figurine" pour ajouter une contrainte de clé étrangère avec la table "weapon" :

  ALTER TABLE figurine ADD CONSTRAINT fk_id_weapon FOREIGN KEY (weapon_id) REFERENCES weapon(id);

Mettre la table "weapon" en relation avec la table "figurine" :
id 1 = 2
id 8 =5
id 4 = 4 

  UPDATE figurine SET weapon_id=1 WHERE nom = "Thor";
  UPDATE figurine SET weapon_id=4 WHERE nom = "Hulk";
  UPDATE figurine SET weapon_id=5 WHERE nom = "Black Panther";
  UPDATE figurine SET weapon_id=2 WHERE nom = "Captain America";
    UPDATE figurine SET weapon_id=2 WHERE id=2;


Afficher tous les avengers :

SELECT*FROM figurine INNER JOIN weapon ON weapon.id=weapon_id;

-- Récuperer le nom des avengers et le nom de leurs armes dont l'année de sortie est supérieur à 2010

SELECT figurine.nom, weapon.nom FROM figurine INNER JOIN weapon ON weapon.id=weapon_id WHERE annee_sortie>2010;

SELECT nom FROM figurine WHERE weapon_id IS NULL;

 ````
