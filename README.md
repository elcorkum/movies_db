CREATE DATABASE IF NOT EXISTS movies_db;
USE movies_db;

CREATE TABLE movies(
title varchar(150) NOT NULL DEFAULT '',
runtime int UNSIGNED NOT NULL DEFAULT 0,
genre varchar(20) NOT NULL DEFAULT '',
imdb_score decimal(2, 1) UNSIGNED NOT NULL DEFAULT 00.0,
rating varchar(10) NOT NULL DEFAULT ''
);

INSERT INTO movies
VALUES
('Howard the Duck', 110, 'Sci-Fi', 4.6, 'PG'),
('Lavalantula', 83, 'Horror', 4.7, 'TV-14'),
('Starship Troopers', 129, 'Sci-Fi', 7.2, 'PG-13'),
('Waltz with Bashir', 90, 'Documentary', 8.0, 'R'),
('Spaceballs', 96, 'Comedy', 7.1, 'PG'),
('Monsters Inc.', 92, 'Animation', 8.1, 'G');

INSERT INTO movies VALUES
('Minions: The Rise of Gru', 87, 'Animation', 6.5, 'PG'),
('The Princess Bride', 98, 'Adventure', 8.0, 'PG')
;

SELECT *
FROM movies
WHERE genre = 'Sci-Fi'
;

SELECT *
FROM movies
WHERE imdb_score >= 6.5
;

SELECT *
FROM movies
WHERE (rating = 'G' OR rating = 'PG') AND runtime < 100
;

SELECT AVG(runtime)
FROM movies
WHERE imdb_score < 7.5
GROUP BY genre
;

UPDATE movies
SET rating = 'R'
WHERE title = 'Starship Troopers'
;

ALTER TABLE movies
ADD COLUMN id_number int(10) UNSIGNED PRIMARY KEY AUTO_INCREMENT FIRST;

SELECT id_number, rating FROM movies
WHERE genre = 'Horror' OR genre = 'Documentary'
;

SELECT rating AS 'IMDB Scores by Rating', AVG(imdb_score), MIN(imdb_score), MAX(imdb_score)
FROM movies
GROUP BY rating
;

SELECT rating AS 'IMDB Scores by Rating', AVG(imdb_score), MIN(imdb_score), MAX(imdb_score)
FROM movies
GROUP BY rating
HAVING COUNT(*) > 1
;


DELETE FROM movies
WHERE rating = 'R'
;

DROP TABLE movies;

DROP DATABASE movies_db;