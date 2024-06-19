### Exercice avec une Base de Données pour une Plateforme de Sport

Dans cet exercice, nous allons créer une base de données pour gérer des équipes, des joueurs, des matchs et des scores dans une ligue sportive.

## Étapes à Suivre

### 1. Créez la Base de Données `sports_db`

CREATE DATABASE sports_db;

### 2. Utilisez la Base de Données `sports_db`

USE sports_db;

### 3. Créez les Tables

#### a. Table "team"


CREATE TABLE team (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR (255),
    ville VARCHAR (255),
    coach VARCHAR (255)
);
    - La table "team" stockera les détails des équipes. Elle contiendra les colonnes suivantes:
        - id: Identifiant de l'équipe
        - nom: Nom de l'équipe
        - ville: Ville de l'équipe
        - coach: Nom du coach de l'équipe

#### b. Table "player"


CREATE TABLE player (

    id INT PRIMARY KEY AUTO_INCREMENT,
    nom Varchar(255),
    equipe_id  INT,
    prenom VARCHAR(255),
    date_naissance DATE,
    position VARCHAR(255),

   FOREIGN KEY (equipe_id) REFERENCES team(id)
);
    - La table "player" stockera les détails des joueurs. Elle contiendra les colonnes suivantes:
        - id: Identifiant du joueur
        - nom: Nom du joueur
        - prenom: Prénom du joueur
        - date_naissance: Date de naissance du joueur
        - position: Poste du joueur (Attaquant, Défenseur, Milieu de terrain, Gardien de but)
        - equipe_id: Identifiant de l'équipe à laquelle le joueur appartient (clé étrangère)

#### c. Table "match"

CREATE TABLE `match`(

    id INT PRIMARY KEY AUTO_INCREMENT,
    date_match DATE,
    equipe_domicile_id INT,
    equipe_exterieur_id INT,

    FOREIGN KEY (equipe_domicile_id) REFERENCES team(id),
    FOREIGN KEY (equipe_exterieur_id) REFERENCES team(id)
);

    - La table "match" stockera les détails des matchs joués par les équipes. Elle contiendra les colonnes suivantes:
        - id: Identifiant du match
        - date_match: Date du match
        - equipe_domicile_id: Identifiant de l'équipe à domicile (clé étrangère)
        - equipe_exterieur_id: Identifiant de l'équipe à l'extérieur (clé étrangère)

#### d. Table "score"


CREATE TABLE score (

    id INT PRIMARY KEY AUTO_INCREMENT,
    match_id INT,
    equipe_id INT,
    points INT,

    FOREIGN KEY (match_id) REFERENCES `match`(id),
    FOREIGN KEY (equipe_id) REFERENCES team(id)
);
    - La table "score" stockera les points marqués par chaque équipe dans un match. Elle contiendra les colonnes suivantes:
        - id: Identifiant du score
        - match_id: Identifiant du match associé (clé étrangère)
        - equipe_id: Identifiant de l'équipe associée (clé étrangère)
        - points: Nombre de points marqués par l'équipe

### 4. Insérez des Données dans les Tables

#### a. Insertion des Équipes

```sql

INSERT INTO team (nom, ville, coach) VALUES
('Lions', 'New York', 'John Smith'),
('Tigers', 'Los Angeles', 'Mike Johnson'),
('Bears', 'Chicago', 'Tom Brown'),
('Wolves', 'Houston', 'James Williams'),
('Eagles', 'Philadelphia', 'Robert Jones'),
('Sharks', 'Miami', 'David Wilson'),
('Panthers', 'Dallas', 'Chris Lee'),
('Hawks', 'Atlanta', 'Mark Taylor'),
('Dragons', 'San Francisco', 'Luke Harris'),
('Knights', 'Boston', 'Paul White');
```

#### b. Insertion des Joueurs

```sql

INSERT INTO player (nom,prenom, date_naissance,position,equipe_id)VALUES
('Doe', 'John', '1990-01-01', 'Attacker', 1),
('Smith', 'Emma', '1992-02-15', 'Defender', 1),
('Johnson', 'Michael', '1988-03-30', 'Midfielder', 2),
('Brown', 'Olivia', '1994-04-25', 'Goalkeeper', 2),
('Taylor', 'Sophia', '1996-05-10', 'Attacker', 3),
('Anderson', 'Liam', '1989-06-20', 'Defender', 3),
('Clark', 'Ava', '1995-07-05', 'Midfielder', 4),
('Lewis', 'Noah', '1991-08-15', 'Goalkeeper', 4),
('Walker', 'Mia', '1993-09-25', 'Attacker', 5),
('Hall', 'Elijah', '1987-10-30', 'Defender', 5),
('Martinez', 'Isabella', '1990-11-12', 'Midfielder', 6),
('Garcia', 'Liam', '1986-12-01', 'Goalkeeper', 6),
('Hernandez', 'Emma', '1992-01-14', 'Attacker', 7),
('Lopez', 'Mason', '1993-02-18', 'Defender', 7),
('Gonzalez', 'Ethan', '1994-03-22', 'Midfielder', 8),
('Wilson', 'Sophia', '1995-04-29', 'Goalkeeper', 8),
('Martinez', 'Ava', '1987-05-31', 'Attacker', 9),
('Anderson', 'Noah', '1998-06-28', 'Defender', 9),
('Thomas', 'Mia', '1999-07-15', 'Midfielder', 10),
('Taylor', 'Oliver', '2000-08-16', 'Goalkeeper', 10);
```

#### c. Insertion des Matchs

```sql
INSERT INTO `match`(date_match, equipe_domicile_id, equipe_exterieur_id)VALUES
('2023-01-01', 1, 2),
('2023-01-05', 3, 4),
('2023-01-10', 1, 3),
('2023-01-15', 4, 5),
('2023-01-20', 2, 5),
('2023-01-25', 6, 7),
('2023-02-01', 8, 9),
('2023-02-05', 10, 1),
('2023-02-10', 2, 3),
('2023-02-15', 4, 6);
```

#### d. Insertion des Scores

```sql

INSERT INTO score(match_id, equipe_id,points) VALUES
(1, 1, 3),
(1, 2, 2),
(2, 3, 1),
(2, 4, 1),
(3, 1, 2),
(3, 3, 3),
(4, 4, 0),
(4, 5, 4),
(5, 2, 1),
(5, 5, 3),
(6, 6, 2),
(6, 7, 2),
(7, 8, 1),
(7, 9, 3),
(8, 10, 0),
(8, 1, 1),
(9, 2, 2),
(9, 3, 4),
(10, 4, 1),
(10, 6, 3);
```

### 5. Créez un Utilisateur pour la Base de Données

    - Nom d'Utilisateur: sports_user
    - Mot de Passe: password


    CREATE USER 'sports_user'@'%' IDENTIFIED BY 'paswword';

### 6. Donnez les Privilèges à l'Utilisateur

    - Privilèges: ALL PRIVILEGES
    - Base de Données: sports_db

   GRANT ALL PRIVILEGES ON sports_db.* TO 'sports_user'@'%';
   

### 7. Exportez la Base de Données

    -   Utilisez la commande `mysqldump` pour exporter la base de données dans un fichier SQL.

### Requêtes à Réaliser

1. Affichez les équipes et leurs villes respectives.

SELECT nom, ville FROM team;

2. Affichez les joueurs et leurs équipes respectives, triés par nom de joueur.

SELECT player.nom, player.prenom, team.nom AS equipe FROM player JOIN team ON player.equipe_id =team.id ORDER BY player.nom;


3. Affichez les matchs et les équipes participantes, triés par date de match.

SELECT team.nom AS equipe_domicile, t.nom AS equipe_ext, date_match FROM `match` AS m INNER JOIN team ON m.equipe_domicile_id=team.id INNER JOIN team t ON m.equipe_exterieur_id=t.id ORDER BY date_match ;

4. Affichez les scores de chaque match, triés par match_id.

SELECT match_id, equipe_id, points FROM score ORDER BY match_id;


5. Affichez les équipes avec le nombre total de points marqués, triées par nombre de points décroissant.

SELECT team.nom, SUM(points) FROM score INNER JOIN team ON score.equipe_id=team.id GROUP BY equipe_id ORDER BY SUM(points) DESC;

6. Affichez les joueurs d'une équipe spécifique, triés par position.

SELECT player.nom, prenom, team.nom FROM player INNER JOIN team ON equipe_id=team.id ORDER BY position;

7. Affichez les matchs où les scores des deux équipes sont égaux.
SELECT t1.nom,s1.points,s2.points, t2.nom FROM `match`
INNER JOIN team t1 ON match.equipe_domicile_id=t1.id
INNER JOIN team t2 ON match.equipe_exterieur_id=t2.id
INNER JOIN score s1 ON t1.id=s1.equipe_id AND  match.id= s1.match_id
INNER JOIN score s2 ON t2.id=s2.equipe_id AND  match.id= s2.match_id
WHERE s1.points=s2.points;


8. Affichez les matchs joués par une équipe spécifique, triés par date de match.
9. Affichez les équipes qui ont marqué plus de 2 points dans un match, triées par nombre de points.
10. Affichez les joueurs qui sont des attaquants, triés par date de naissance.

### Requêtes Additionnelles

1. Affichez les joueurs triés par date de naissance puis par nom.
2. Affichez les matchs triés par date de match puis par équipe domicile.
3. Affichez les scores triés par nombre de points puis par match_id.
4. Affichez les équipes triées par ville puis par nom.
5. Affichez les joueurs triés par équipe_id puis par position.

### Requêtes SQL pour les Modifications

#### 1. Requêtes `UPDATE`

1. **Mettre à jour le nom du coach de l'équipe 'Lions'**

    - Définir le nouveau nom du coach comme 'Samuel Jackson'

2. **Mettre à jour la ville de l'équipe 'Tigers'**

    - Définir la nouvelle ville comme 'San Diego'

3. **Mettre à jour la position d'un joueur spécifique**

    - Mettre à jour la position de 'John Doe' en 'Midfielder'

#### 2. Requêtes `DELETE`

1. **Supprimer une équipe spécifique**

    - Supprimer l'équipe 'Sharks'

2. **Supprimer un joueur spécifique**

    - Supprimer le joueur 'Emma Smith'

#### 3. Nouvelle Insertion

1. **Insertion d'un nouveau joueur**

    - Insérer un nouveau joueur nommé 'Henry Miller' né le 12 mars 2001, jouant en tant que défenseur pour l'équipe 'Lions'.

#### 4. Modifications de Tables

1. **Ajouter une nouvelle colonne `email` à la table `player`**

    - La colonne `email` doit être de type `VARCHAR(100)`.

2. **Modifier le type de la colonne `points` dans la table `score` pour accepter des décimales**

    - Modifier le type de données de la colonne `points` en `DECIMAL(5,2)`.
