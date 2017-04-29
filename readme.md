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

## Adding data to the db using INSERT INTO dbname(colnames) VALUES (data);

* INSERT INTO tablename (column1,column2...) VALUES (data1,data2...);
* INSERT INTO movies (id,title,genre,duration) VALUES (5, 'The Trooper', 'Action', 90);
* INSERT INTO movies VALUES (5, 'The trooper', 'Action', 90); //This is a better way as all the columns are being used so use this instead of naming all columns as above.
* INSERT INTO movies (title,duration) VALUES ('The Hero', 93); //id column wont be NULL, it will be automatically filled with 6 as its the primary key which is a unique col and will have a different value for every entry. It will be automatically incremented.
* genre in the above data will be NULL which is a placeholder for unknown or unavailable data.

## Changing data using UPDATE dbname SET colToChange = newValue WHERE ....

* The where clause is used to pinpoint the location of the update.
* UPDATE movies SET genre = 'Romance' WHERE id=4;
* UPDATE movies SET genre = 'Romance', duration = 94 WHERE id=4;
* Change multiple rows using WHERE clause eg. UPDATE movies SET genre = 'Romance' WHERE id = 4 OR id = 6;

## Remove data using DELETE FROM dbname WHERE ....

* DELETE removes rows from the table based on the WHERE clause.
* DELETE FROM movies WHERE id=4;
* DELETE FROM movies; //This will delete everything
* Delete multiple rows by -> DELETE FROM movies WHERE duration > 90;

## To CREATE or DROP(delete) a new Database/table

* CREATE DATABASE Ravi Theatres; //Creates a new empty db
* DROP DATABASE Ravi's X Theatres; //To remove a database
* CREATE TABLE tableName (colName1 Datatype, colName2 Datatype, ColName3 Datatype ...); //Creates a new table inside Ravi Theatres db
* CREATE TABLE movies (id int, title varchar(50), genre varchar(15), duration int);
* DROP TABLE tableName; //to remove a table from the db.

## Manipulating Database using ALTER TABLE

* To add, remove, modify columnns in a table.
* ALTER TABLE tableName ADD COLUMN columnName datatype; //To add a new column to a table
* ALTER TABLE movies ADD COLUMN ratings int; 
* ALTER TABLE tablName DROP COLUMN columnName; //To remove a column from the table
* ALTER TABLE movies DROP COLUMN ratings;


## Common Aggregate Functions

* SELECT count(col_name) FROM tableName;
* SELECT sum(col_name) FROM tableName;
* SELECT avg(col_name) FROM tableName;
* SELECT max(col_name) FROM tableName;
* SELECT min(col_name) FROM tableName;
* The last 4 work only if all entries are int.
* To count all the rows -> SELECT count ( * ) FROM movies; // asterix will include rows with NULL values as well. Else, use below statement.
* To count all rows with a title not NULL -> SELECT count(title) FROM movies;
* SELECT max(tickets), min(tickets) FROM movies;
* SELECT count ( * ) FROM Actors WHERE country='USA'; 

## Aggregates within clauses

* SELECT col_name, aggregate_func(col_name) FROM tableName GROUP BY col_name;
* SELECT genre, sum(cost) FROM movies GROUP BY genre; //Will give total cost of movies according to the genre.
* SELECT genre, sum(cost) FROM movies GROUP BY genre HAVING count( * ) > 1;
* SELECT genre, sum(cost) FROM movies WHERE cost >= 100000 GROUP BY genre HAVING count( * ) > 1;
* SELECT country, sum(salary) FROM Actors WHERE role = 'supporting' GROUP BY country HAVING count( * ) > 1; 
