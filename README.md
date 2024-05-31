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

mysql> select * from movies_view
    -> where Genre = 'Sci-Fi';
+-------------------+---------+--------+------------+--------+
| Title             | Runtime | Genre  | IMDB_Score | Rating |
+-------------------+---------+--------+------------+--------+
| Howard the Duck   |     110 | Sci-Fi |        4.6 | PG     |
| Starship Troopers |     129 | Sci-Fi |        7.2 | R      |
+-------------------+---------+--------+------------+--------+
