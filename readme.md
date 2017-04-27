# SQL Commands

## SELECT FROM basics

* SELECT title,genre FROM movies;
* SELECT * FROM movies; (will select everything from the movies database).

## SELECT FROM database WHERE

* SELECT title FROM movies WHERE id=2; ( will select title from movies where id is 2, will check throughout the table for duplicate ids)
* SELECT * FROM movies WHERE title='The Kid'; (will select everything from movies where title is 'The Kid', will lookup entire table)

## SELECT FROM database ORDER BY

* SELECT title FROM movies ORDER BY duration; (default is ascending order)
* SELECT title FROM movies ORDER BY duration DESC;

## Operators

* SELECT title FROM movies WHERE duration > 100;
* SELECT title FROM movies WHERE duration < 100;
* SELECT title FROM movies WHERE duration >= 100;
* SELECT title FROM movies WHERE duration <= 100;
* SELECT title FROM movies WHERE duration <> 100; (is not equal to)
* SELECT title FROM movies WHERE duration > 100 AND id = 2;
* SELECT title FROM movies WHERE duration > 100 OR id=4;
* SELECT item, price, size FROM concessions WHERE item = 'Popcorn' OR item = 'Soda' ORDER BY price DESC;

