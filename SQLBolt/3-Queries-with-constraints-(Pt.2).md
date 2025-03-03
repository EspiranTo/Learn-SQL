# SQLBolt
There are queries for section 3 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_constraints_pt_2).

## Queries with constraints (Pt. 2)

1. 
Find all the Toy Story movies.
```sql
  SELECT title FROM movies
    WHERE title LIKE 'Toy Story%'
```
2. 
Find all the movies directed by John Lasseter.
```sql
  SELECT title FROM movies
    WHERE director = 'John Lasseter'
```
3. 
Find all the movies (and director) not directed by John Lasseter.
```sql
  SELECT title, director FROM movies
    WHERE director <> 'John Lasseter'
```
4. 
Find all the WALL-* movies.
```sql
  SELECT title FROM movies
    WHERE title LIKE 'WALL-%'
```