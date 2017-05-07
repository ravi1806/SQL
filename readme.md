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

## Constraints NOT NULL UNIQUE PRIMARY KEY

* CREATE TABLE Promotions ( id int, name varchar(50) NOT NULL, category varchar(20) ); //Here NOT NULL is a constraint which will make sure that that column doenst have an empty value or NULL or it will throw an error.
* CREATE TABLE Promotions ( id int, name varchar(50) NOT NULL UNIQUE, category varchar(20) );. This method is called **Column Constraint** //Unique will make sure it isnt duplicated
* Another way of assigning constraints is to give them custom names eg. below
* CREATE TABLE Promotions (id int, name varchar(50), category varchar(20), CONSTRAINT custom_unique_name UNIQUE (name); // where name is the col_name that needs to be applied upon. This method is called **Table Constraint** .
* CREATE TABLE Promotions (id int, name varchar(50), category varchar(20), CONSTRAINT custom_unique_name UNIQUE (name, category);
* CREATE TABLE Promotions (id int PRIMARY KEY, name varchar(50), category varchar(20) ); //Primary key can be assigned only once per table.

## Creating valid references between two tables usig FORIEGN KEY, Orphan records and CHECK Constraint

* When creating the reference we must use the naming convention as referencedTablenameSingularized_columnname (from a Movies table, into a Promotions table, it will named as movie_id )
* We use a FOREIGN_KEY constraint to avoid insertion of invalid data into a table and to avoid creation of ORPHAN records. (we can insert into movie_id some id which may not be present in the MOVIES table, to avoid it, we must use the FOREIGN KEY CONSTRAINT.
* To create a foreign key in Promotions table, it is neccessary that a movies table with id col exists. eg. below
* CREATE TABLE Movies ( id int PRIMARY KEY, title varchar(20) NOT NULL UNIQUE ); //This needs to exist before creating a reference from here
* CREATE TABLE Promotions ( id int PRIMARY KEY, movie_id int REFERENCES movies(id), name varchar(50), category varchar(15) ); //REFERENCES movies(id) will create the foreign key. A shorter way will be REFERENCES movies.
* Table constraint method is -> CREATE TABLE Promotions ( FOREIGN KEY (movie_id) REFERENCES movies );
* **ORPHAN** Records are child records with a forieng key to a parent record that has been deleted.
* colName int CHECK (duration > 0) will make sure its value is not negative.

## Normalization

* Eg. A movies table with id,title,genre and duration. 
* When a movie has two or more genre, it should not be written in one column as it defies the rule 1 of Normal Form.
* First Normal Form Rule: Tables must not contain repeating groups of data in one column.
* Second Normal Form Rule: Tables must not contain redundancy.
* To avoid redundancy we must contain two new tables and a third table joining the two of them.
* So drop the column genre from the Movies table using ALTER TABLE tableName DROP COLUMN colName
* Create a new Genres table with its own id and genre.
* Make a third table to link the above two tables with naming convention of firstTable_secondTable. So make table Movies_Genres
* This Movies_Genres table will contain two cols of movies_id and genre_id as Foreign keys from Movies and Genres Table.
* Refer to personal video 'sql12' for more.

## 3 Different Types of Table Relationships

* One to One
* One to Many
* Many to Many


## Inner Joins

* Given a table Movies with id,title,genre,duration and another table Reviews with id,review and movie_id(FK).
* When we need to fetch data from muliple table, in this case to get a list of reviews for all and to get their titles we will 
* Fetch all the reviews by SELECT reviews, movie_id FROM Reviews;
* Fetch all the movie associaited titles by SELECT title FROM Movies WHERE id in (1,3,4); //which is a shortcut for WHERE id=1 OR id=3 OR id=4;
* We can achieve this using just one query. SELECT * FROM OneTable INNER JOIN SecondTable ON OneTable.ColName = SecondTable.colName;
* So for above eg. we can write SELECT * FROM Movies INNER JOIN Reviews ON Movies.id = Reviews.movie_id; OR the otherway around like
* SELECT * FROM Reviews INNER JOIN Movies ON Reviews.movie_id = Movies.id;
* But we dont want all the data from these tables, we only need title and reviews so use SELECT tablOne.colName, tablTwo.colName FROM...
* SELECT Movies.title, Reviews.review FROM Movies INNER JOIN Reviews ON Movies.id = Reviews.movie_id

* In Normalization we had a MOVIES table with id,title,duration and genre table with id and name and a joining table MOVIES_GENRE with movie_id and genre_id(many to many).
* Now to find all genres of a Movie we had to write 3 different queries eg.
* SELECT id FROM Movies WHERE title = 'Peter Pan'; , SELECT genre_id FROM Movies_Genre WHERE id = 2; SELECT name FROM genre WHERE id IN (2,3); //this query tells the name of the genre which has id 2 or id 3.
* All this can be written in one query as following.
* SELECT Movies.title, Genre.name FROM Movies INNER JOIN Movies_Genre ON Movies.id = Movies_Genre.movie_id INNER JOIN Genre ON Movies_Genre.genre_id = Genre.id WHERE title = 'Peter Pan';

* Question: Join the Movies table with the Rooms table so that we only fetch movies that have an associated room. Let's get a little more specific, and only return the movie title, the id for the room, and number of seats in the theatre. Now, let's filter the results more by only showing theatres with more than 75 seats. Remember, the WHERE clause should go after the JOIN syntax. Finally, let's sort the result by seats in the theatre from most to least seats.
* Ans: SELECT Movies.title, Rooms.id, Rooms.seats From Movies INNER JOIN Rooms ON Movies.id = Rooms.movie_id WHERE seats > 75 ORDER BY seats DESC;

* Question: First, join the Actors table with the Actors_Movies table so that only actors participating in movies are returned on the result.Next, create another INNER JOIN from the Actors_Movies table to the Movies table so that our result shows information about the movies. Now change the query to only fetch actor names and movie titles. Lastly, let's sort this query by movie title, alphabetically.
* Ans: SELECT Actors.name, Movies.title FROM Actors INNER JOIN Actors_Movies ON Actors.id = Actors_Movies.actor_id INNER JOIN Movies ON Actors_Movies.movie_id = Movies.id ORDER BY Movies.title;

## ALIAS

* We can write alias for queries eg.
* SELECT Movies.title AS films, Reviews.review AS reviews.
* We can drop AS and write in shortcut -> SELECT Movies.title films, Revies.review reviews. //use " " for alias with space
* WE can use Table Aliases for the Table Names eg.
* SELECT m.title, r.review FROM Movies m INNER JOIN Reviews r ON m.id = r.movie_id ORDER BY m.title; //HERE we defined the ALIAS at FROM MOVIES m and INNER JOIN Reviews r

* Question: First, change the query to output "Movie Title" instead of just title on the result.Next, change the id field to print "Theatre Number".Now, let's use table aliases to shorten the query. Alias Rooms to use "r" and Movies to "m".
* Ans: SELECT m.title "Movie Title", r.id "Theatre Number", r.seats FROM Movies m INNER JOIN Rooms r ON m.id = r.movie_id WHERE r.seats > 75 ORDER BY r.seats desc;

