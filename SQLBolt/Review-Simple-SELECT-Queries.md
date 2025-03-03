# SQLBolt
There are queries for section SQL Review from website [SQLBolt](https://sqlbolt.com/lesson/select_queries_review).

## Simple SELECT Queries

1. 
List all the Canadian cities and their populations.
```sql
  SELECT city, population FROM north_american_cities
    WHERE country = 'Canada'
```
2. 
Order all the cities in the United States by their latitude from north to south.
```sql
  SELECT city FROM north_american_cities
    WHERE country = 'United States'
    ORDER BY latitude DESC
```
3. 
List all the cities west of Chicago, ordered from west to east.
```sql
  SELECT city FROM north_american_cities
    WHERE longitude <
      ( SELECT longitude FROM north_american_cities
        WHERE city = 'Chicago')
    ORDER BY longitude ASC
```
4. 
List the two largest cities in Mexico (by population).
```sql
  SELECT city FROM north_american_cities
    WHERE country = 'Mexico'
    ORDER BY population DESC
    LIMIT 2
```
5. 
List the third and fourth largest cities (by population) in the United States and their population.
```sql
  SELECT city, population FROM north_american_cities
    WHERE country = 'United States'
    ORDER BY population DESC
    LIMIT 2 OFFSET 2
```