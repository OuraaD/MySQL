# Exercice avec une Base de Données pour une Plateforme de Musique

Dans cet exercice, nous allons créer une base de données pour gérer des artistes, des albums, des chansons et des utilisateurs dans une plateforme de musique.

## Étapes à Suivre

### 1. Créez la Base de Données `music_db`

CREATE DATABASE music_db;

### 2. Utilisez la Base de Données `music_db`

USE music_db;

### 3. Créez les Tables

#### a. Table "artist"

CREATE TABLE artist (

    id INT PRIMARY KEY AUTO_INCREMENT,
    nom VARCHAR (255),
    pays VARCHAR(255),
    date_debut DATE
);

#### b. Table "album"

CREATE TABLE album(
    id INT PRIMARY KEY AUTO_INCREMENT ,
    artiste_id INT,
    titre VARCHAR (255),
    annee_sortie INT(4),
    genre VARCHAR(255),
    FOREIGN KEY (artiste_id) REFERENCES artist(id)
);


#### c. Table "song"

CREATE TABLE song (

    id INT PRIMARY KEY AUTO_INCREMENT,
    album_id INT,
    titre VARCHAR(255),
    duree INT, 
    
FOREIGN KEY (album_id) REFERENCES album(id) 
);


#### d. Table "user"

CREATE TABLE user(

    id INT PRIMARY KEY AUTO_INCREMENT ,
    nom_utilisateur VARCHAR (255),
    email VARCHAR (255),
    mot_de_passe VARCHAR(255)

);


#### e. Table "playlist"
CREATE TABLE playlist(

    id INT PRIMARY KEY AUTO_INCREMENT,
    utilisateur_id INT,
    nom VARCHAR(255),
    date_creation DATE,
   FOREIGN KEY (utilisateur_id) REFERENCES user(id)

);


#### f. Table "playlist_song"

    CREATE TABLE playlist_song(

    id INT PRIMARY KEY AUTO_INCREMENT,
    playlist_id INT,
    chanson_id INT,
    FOREIGN KEY (playlist_id) REFERENCES playlist(id),
    FOREIGN KEY (chanson_id) REFERENCES song(id)

    );

### 4. Insérez des Données dans les Tables

#### a. Insertion des Artistes

```sql

INSERT INTO artist (nom, pays, date_debut) VALUES
('The Beatles', 'UK', '1960-01-01'),
('Beyoncé', 'USA', '1997-01-01'),
('Eminem', 'USA', '1996-01-01'),
('Adele', 'UK', '2006-01-01'),
('Drake', 'Canada', '2006-01-01');
```

#### b. Insertion des Albums

```sql

INSERT INTO album( artiste_id, titre, annee_sortie, genre) VALUES
(1, 'Abbey Road', 1969, 'Rock'),
(1, 'Sgt. Pepper\'s Lonely Hearts Club Band', 1967, 'Rock'),
(2, 'Lemonade', 2016, 'Pop'),
(3, 'The Eminem Show', 2002, 'Rap'),
(4, '25', 2015, 'Pop'),
(5, 'Scorpion', 2018, 'Rap');
```

#### c. Insertion des Chansons

```sql
INSERT INTO song (album_id, titre, duree) VALUES
(1, 'Come Together', 259),
(1, 'Something', 182),
(2, 'Sgt. Pepper\'s Lonely Hearts Club Band', 122),
(2, 'Lucy in the Sky with Diamonds', 207),
(3, 'Formation', 210),
(3, 'Sorry', 200),
(4, 'Without Me', 290),
(4, 'Cleanin\' Out My Closet', 297),
(5, 'Hello', 295),
(5, 'Send My Love (To Your New Lover)', 223),
(6, 'God\'s Plan', 198),
(6, 'In My Feelings', 217);
```

#### d. Insertion des Utilisateurs

```sql

INSERT INTO user(nom_utilisateur, email, mot_de_passe) VALUES
('john_doe', 'john.doe@example.com', 'password123'),
('jane_smith', 'jane.smith@example.com', 'password123'),
('michael_johnson', 'michael.johnson@example.com', 'password123');
```

#### e. Insertion des Playlists

```sql

INSERT INTO playlist (utilisateur_id, nom, date_creation) VALUES
(1, 'Rock Classics', '2022-01-01'),
(2, 'Rap Hits', '2022-02-01'),
(3, 'Pop Favorites', '2022-03-01');
```

#### f. Insertion des Chansons dans les Playlists

```sql

INSERT INTO playlist_song(playlist_id, chanson_id) VALUES
(1, 1), (1, 2), (1, 3), (1, 4),
(2, 7), (2, 8), (2, 11), (2, 12),
(3, 5), (3, 6), (3, 9), (3, 10);
```

### Requêtes Supplémentaires

1. Affichez les albums et leurs artistes respectifs.

SELECT nom, titre  FROM album INNER JOIN artist ON album.artiste_id = artist.id;



2. Affichez les chansons et leurs albums respectifs, triées par titre de chanson.

SELECT song, titre FROM song INNER : JOIN album ON song.album_id = album.id ORDER BY song.titre;


3. Affichez les playlists et le nombre de chansons dans chaque playlist, triées par nom de playlist.

SELECT playlist.nom AS Playlist, COUNT(playlist_song.chanson_id) AS NombreDeChansons FROM playlist INNER JOIN playlist_song ON playlist.id = playlist_song.playlist_id GROUP BY playlist.nom ORDER BY playlist.nom;

4. Affichez les utilisateurs et le nombre de playlists qu'ils ont créées.

SELECT user.nom_utilisateur AS Utilisateur, COUNT(playlist.id) AS NombreDePlaylists
FROM user INNER JOIN playlist ON user.id = playlist.utilisateur_id GROUP BY user.nom_utilisateur;

5. Affichez les chansons d'une playlist spécifique, triées par titre de chanson.



6. Affichez les artistes avec le nombre total de chansons qu'ils ont.

SELECT artist.nom AS Artiste, COUNT(song.id) AS NombreDeChansons FROM artist JOIN album ON artist.id = album.artiste_id JOIN song ON album.id = song.album_id GROUP BY artist.nom;



7. Affichez les chansons dont la durée est supérieure à 300 secondes, triées par durée décroissante.

SELECT* FROM song WHERE duree > 300 ORDER BY duree DESC;


8. Affichez les albums sortis après l'année 2000, triés par année de sortie.

SELECT * FROM album WHERE annee_sortie > 2000 ORDER BY annee_sortie;


9. Affichez les utilisateurs et les chansons qu'ils ont dans leurs playlists, triées par nom d'utilisateur.

SELECT user.nom_utilisateur, song.titre FROM user INNER JOIN playlist pl ON user.id=pl.utilisateur_id INNER JOIN playlist_song pls ON pls.playlist_id=pl.id INNER JOIN song ON pls.chanson_id=song.id ORDER BY user.nom_utilisateur;

10. Affichez les playlists créées après le 1er janvier 2022, triées par date de création.

SELECT nom, date_creation FROM playlist WHERE date_creation >2022-01-01 ORDER BY date_creation;

Utilisez ces requêtes pour pratiquer les jointures, les agrégations, les tris et les limites dans une base de données relationnelle sur le thème de la musique.
