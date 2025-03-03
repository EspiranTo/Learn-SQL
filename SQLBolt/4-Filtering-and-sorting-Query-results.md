# SQLBolt
There are queries for section 4 from website [SQLBolt](https://sqlbolt.com/lesson/filtering_sorting_query_results).

## Filtering and sorting Query results

1. 
List all directors of Pixar movies (alphabetically), without duplicates.
```sql
  SELECT DISTINCT director FROM movies
    ORDER BY director
```
2. 
List the last four Pixar movies released (ordered from most recent to least).
```sql
  SELECT title FROM movies
    ORDER BY year DESC
    LIMIT 4
```
3. 
List the first five Pixar movies sorted alphabetically.
```sql
  SELECT title FROM movies
    ORDER BY title
    LIMIT 5
```
4. 
List the next five Pixar movies sorted alphabetically.
```sql
  SELECT title FROM movies
    ORDER BY title
    LIMIT 5 OFFSET 5
```