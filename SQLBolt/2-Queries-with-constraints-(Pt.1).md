# SQLBolt
There are queries for section 2 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_constraints).

## Queries with constraints (Pt. 1)

1. 
Find the movie with a row id of 6.
```sql
  SELECT title FROM movies
    WHERE id = 6
```
2. 
Find the movies released in the years between 2000 and 2010.
```sql
  SELECT title FROM movies
    WHERE year BETWEEN 2000 AND 2010 
```
3. 
Find the movies not released in the years between 2000 and 2010.
```sql
  SELECT title FROM movies
    WHERE year NOT BETWEEN 2000 AND 2010 
```
4. 
Find the first 5 Pixar movies and their release year.
```sql
  SELECT title, year FROM movies
    WHERE id IN (1, 2, 3, 4, 5)
```