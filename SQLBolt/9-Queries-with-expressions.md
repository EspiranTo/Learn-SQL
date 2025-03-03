# SQLBolt
There are queries for section 9 from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_with_expressions).

## Queries with expressions

1. 
List all movies and their combined sales in millions of dollars.
```sql
  SELECT title, (domestic_sales + international_sales)/1000000 AS Sales FROM movies
    INNER JOIN boxoffice ON movie_id = id
```
2. 
List all movies and their ratings in percent.
```sql
  SELECT title, rating*10 AS Percent FROM movies
    INNER JOIN boxoffice ON movie_id = id
```
3. 
List all movies that were released on even number years.
```sql
  SELECT title FROM movies
    WHERE year % 2 = 0
```