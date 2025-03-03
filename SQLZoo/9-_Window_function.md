There are queries for section 9- from website [SQLZoo](https://sqlzoo.net/wiki/Window_functions).

## Window functions

1. Warming up
Show the lastName, party and votes for the constituency 'S14000024' in 2017.
```sql
  SELECT lastName, party, votes FROM ge
    WHERE constituency = 'S14000024' AND yr = 2017
    ORDER BY votes DESC
```
2. Who won?
Show the party and RANK for constituency S14000024 in 2017. List the output by party.
```sql
  SELECT party, votes,
  RANK() OVER (ORDER BY votes DESC) as posn FROM ge
    WHERE constituency = 'S14000024' AND yr = 2017
    ORDER BY party
```
3. PARTITION BY
Use PARTITION to show the ranking of each party in S14000021 in each year. Include yr, party, votes and ranking (the party with the most votes is 1).
```sql
  SELECT yr, party, votes,
  RANK() OVER (PARTITION BY yr ORDER BY votes DESC) as posn FROM ge
    WHERE constituency = 'S14000021'
    ORDER BY party, yr
```
4. Edinburgh Constituency
Use PARTITION BY constituency to show the ranking of each party in Edinburgh in 2017. Order your results so the winners are shown first, then ordered by constituency.
```sql
  SELECT constituency, party, votes,
  RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) as posn FROM ge
    WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
    AND yr  = 2017
    ORDER BY posn , constituency
```
5. Winners Only
Show the parties that won for each Edinburgh constituency in 2017.
```sql
  SELECT constituency, party
  FROM ( SELECT constituency, party, votes,
         RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn FROM ge
           WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
           AND yr  = 2017
           ORDER BY posn , constituency ) x
    WHERE x.posn = 1
```
6. Scottish seats
Show how many seats for each party in Scotland in 2017.
```sql
  SELECT party, count(*)
  FROM ( SELECT constituency, party
         FROM ( SELECT constituency, party, votes,
                RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn FROM ge
                  WHERE constituency LIKE 'S%' AND yr  = 2017
                  ORDER BY posn , constituency ) x
           WHERE x.posn = 1 ) y
    GROUP BY party
```