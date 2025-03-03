# SQLZoo
There are queries for section 5 from website [SQLZoo](https://sqlzoo.net/wiki/SUM_and_COUNT).

## SUM and COUNT

1. Total world population
Show the total population of the world.
```sql
  SELECT SUM(population) FROM world
```
2. List of continents
List all the continents - just once each.
```sql
  SELECT DISTINCT continent FROM world
```
3. GDP of Africa
Give the total GDP of Africa.
```sql
  SELECT SUM(gdp) FROM world
    WHERE continent = 'Africa'
```
4. Count the big countries
How many countries have an area of at least 1000000?
```sql
  SELECT COUNT(name) FROM world
    WHERE area >= 1000000
```
5. Baltic states population
What is the total population of ('Estonia', 'Latvia', 'Lithuania').
```sql
  SELECT SUM(population) FROM world
    WHERE name IN ('Estonia', 'Latvia', 'Lithuania')
```
6. Counting the countries of each continent
For each continent show the continent and number of countries.
```sql
  SELECT continent, COUNT(name) FROM world
    GROUP BY continent
```
7. Counting big countries in each continent
For each continent show the continent and number of countries with populations of at least 10 million.
```sql
  SELECT continent, COUNT(name) FROM world
    WHERE population >= 10000000
    GROUP BY continent
```
8. Counting big continents
List the continents that have a total population of at least 100 million.
```sql
  SELECT continent FROM world
    GROUP BY continent
    HAVING SUM(population) >= 100000000
```