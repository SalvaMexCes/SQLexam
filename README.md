# SQLexam

mysql> select * from movies_view;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
| Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
| Starship Troopers |     129 | Sci-Fi      |        7.2 | R      |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| Deadpool          |     120 | Comedy      |        9.0 | R      |
| Wolverine         |     130 | Action      |        8.6 | PG-13  |
+-------------------+---------+-------------+------------+--------+
8 rows in set (0.02 sec)




Create a query to find all movies in the Sci-Fi genre.

mysql> select * from movies_view
    -> where Genre = 'Sci-Fi';
+-------------------+---------+--------+------------+--------+
| Title             | Runtime | Genre  | IMDB_Score | Rating |
+-------------------+---------+--------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi |        4.6 | PG     |
| Starship Troopers |     129 | Sci-Fi |        7.2 | R      |
+-------------------+---------+--------+------------+--------+




Create a query to find all films that scored at least a 6.5 on IMDB

mysql> select * from movies_view
    -> where IMDB_Score >= 6.5;
+-------------------+---------+-------------+------------+--------+
| Title             | Runtime | Genre       | IMDB_Score | Rating |
+-------------------+---------+-------------+------------+--------+
| Starship Troopers |     129 | Sci-Fi      |        7.2 | R      |
| Waltz With Bashir |      90 | Documentary |        8.0 | R      |
| Spaceballs        |      96 | Comedy      |        7.1 | PG     |
| Monsters Inc.     |      92 | Animation   |        8.1 | G      |
| Deadpool          |     120 | Comedy      |        9.0 | R      |
| Wolverine         |     130 | Action      |        8.6 | PG-13  |
+-------------------+---------+-------------+------------+--------+
6 rows in set (0.00 sec)




For parents who have young kids, but who don't want to sit through long children's movies, create a query to find all of the movies rated G or PG that are less than 100 minutes long.

mysql> select * from movies_view
    -> where Rating='G' or Rating ='PG' and Runtime <100;
+---------------+---------+-----------+------------+--------+
| Title         | Runtime | Genre     | IMDB_Score | Rating |
+---------------+---------+-----------+------------+--------+
| Spaceballs    |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc. |      92 | Animation |        8.1 | G      |
+---------------+---------+-----------+------------+--------+
2 rows in set (0.00 sec)




Create a query to show the average runtimes of movies scoring below a 7.5 on imdb, grouped by their respective genres.

mysql> select avg(Runtime)
    -> from movies_view
    -> where IMDB_Score < 7.5
    -> group by Genre;
+--------------+
| avg(Runtime) |
+--------------+
|     119.5000 |
|      83.0000 |
|      96.0000 |
+--------------+
3 rows in set (0.00 sec)




This time let's find the average, maximum, and minimum IMDB score for movies of each rating.

mysql> select avg(IMDB_Score)
    -> from movies_view
    -> group by Rating;
+-----------------+
| avg(IMDB_Score) |
+-----------------+
|         5.85000 |
|         4.70000 |
|         8.06667 |
|         8.10000 |
|         8.60000 |
+-----------------+

mysql> select min(IMDB_Score)
    -> from movies_view
    -> group by rating;
+-----------------+
| min(IMDB_Score) |
+-----------------+
|             4.6 |
|             4.7 |
|             7.2 |
|             8.1 |
|             8.6 |
+-----------------+
5 rows in set (0.00 sec)

mysql> select max(IMDB_Score)
    -> from movies_view
    -> group by rating;
+-----------------+
| max(IMDB_Score) |
+-----------------+
|             7.1 |
|             4.7 |
|             9.0 |
|             8.1 |
|             8.6 |
+-----------------+




That last query isn't very informative for ratings that only have 1 entry. Use a HAVING COUNT(*) > 1 clause to only show ratings with multiple movies showing.

5 rows in set (0.00 sec)
mysql> SELECT Rating
    -> from movies_view
    -> GROUP BY Rating
    -> HAVING COUNT(*) > 1;
+--------+
| Rating |
+--------+
| PG     |
| R      |
+--------+




Make the movie list more child-friendly. Delete all entries that have a rating of R. Remember to record your queries in a README.md file

mysql> DELETE FROM movies_view
    -> WHERE Rating = 'R';
Query OK, 3 rows affected (0.01 sec)

mysql> select * from movies_view;
+-----------------+---------+-----------+------------+--------+
| Title           | Runtime | Genre     | IMDB_Score | Rating |
+-----------------+---------+-----------+------------+--------+
| Howard the Duck |     110 | Sci-Fi    |        4.6 | PG     |
| Lavalantula     |      83 | Horror    |        4.7 | TV-14  |
| Spaceballs      |      96 | Comedy    |        7.1 | PG     |
| Monsters Inc.   |      92 | Animation |        8.1 | G      |
| Wolverine       |     130 | Action    |        8.6 | PG-13  |
+-----------------+---------+-----------+------------+--------+
5 rows in set (0.00 sec)




Delete the Movies Table

Delete the Database

mysql> DROP TABLE movies_view;
ERROR 1051 (42S02): Unknown table 'movies_db.movies_view'
mysql> DROP TABLE movies;
Query OK, 0 rows affected (0.02 sec)

mysql> DROP DATABASE movies_db;
Query OK, 1 row affected (0.02 sec)




Show the ID number and rating of all of the Horror and Documentary movies in the database. Do this in only one query.

*** Unfortunately I was not able to get this question to work, as my error coming back read "this is not a BASE table". I had to create a custom view for my table last night because I ran into some issues creating it. First I forgot to add the "Title" column for the movies, so my "Title" column in the "base table" was at the last column position, not the first. Then I had a duplicate row i had to remove, but mainly it was switiching the position of the columns, where I had to create a custom table view. ***

The command input I tried executing was as follows:

mysql> ALTER TABLE movies_view ADD COLUMN ID int auto_increment PRIMARY KEY;
