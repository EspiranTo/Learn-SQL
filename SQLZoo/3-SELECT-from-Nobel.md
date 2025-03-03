# SQLZoo
There are queries for section 3 from website [SQLZoo](https://www.sqlzoo.net/wiki/SELECT_from_Nobel_Tutorial).

## SELECT from Nobel

1. Winners from 1950
Change the query shown so that it displays Nobel prizes for 1950.
```sql
  SELECT winner FROM nobel
    WHERE yr = 1950
```
2. 1962 Literature
Show who won the 1962 prize for literature.
```sql
  SELECT winner FROM nobel
    WHERE yr = 1962 AND subject = 'Literature'
```
3. Albert Einstein
Show the year and subject that won 'Albert Einstein' his prize.
```sql
  SELECT yr, subject FROM nobel
    WHERE winner = 'Albert Einstein'
```
4. Recent Peace Prizes
Give the name of the 'peace' winners since the year 2000, including 2000.
```sql
  SELECT winner FROM nobel
    WHERE subject = 'Peace' AND yr >= 2000
```
5. Literature in the 1980's
Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.
```sql
  SELECT * FROM nobel
    WHERE subject = 'Literature' AND yr BETWEEN 1980 AND 1989
```
6. Only Presidents
Show all details of the presidential winners.
```sql
  SELECT * FROM nobel
    WHERE winner IN ('Theodore Roosevelt', 'Thomas Woodrow Wilson', 'Jimmy Carter', 'Barack Obama')
```
7. John
Show the winners with first name John.
```sql
  SELECT winner FROM nobel
    WHERE winner LIKE 'John %'
```
8. Chemistry and Physics from different years
Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.
```sql
  SELECT * FROM nobel
    WHERE subject = 'Physics' AND yr = 1980 OR subject = 'Chemistry' AND yr = 1984
```
9. Early Medicine, Late Literature
Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004).
```sql
  SELECT * FROM nobel
    WHERE subject = 'Medicine' AND yr < 1910 OR subject = 'Literature' AND yr >= 2004
```
### Harder Questions
10. Umlaut
Find all details of the prize won by PETER GRÜNBERG.
```sql
  SELECT * FROM nobel
    WHERE winner = 'Peter Grünberg'
```
11. Apostrophe
Find all details of the prize won by EUGENE O'NEILL.
```sql
  SELECT * FROM nobel
    WHERE winner = 'Eugene O''Neill'
```
12. Knights of the realm
Knights in order.
List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.
```sql
  SELECT winner, yr, subject FROM nobel
    WHERE winner LIKE 'Sir %'
    ORDER BY yr DESC, winner
```
13. Chemistry and Physics last
Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.
```sql
  SELECT winner, subject FROM nobel
    WHERE yr = 1984
    ORDER BY subject IN ('Chemistry', 'Physics'), subject, winner
```