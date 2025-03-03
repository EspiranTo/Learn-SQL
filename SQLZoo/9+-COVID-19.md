There are queries for section 9+ from website [SQLZoo](https://sqlzoo.net/wiki/Window_LAG).

## Window LAG

1. Introducing the covid table
Modify the query to show data from Spain.
```sql
  SELECT name, DAY(whn), confirmed, deaths, recovered FROM covid
    WHERE name = 'Spain' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
    ORDER BY whn
```
2. Introducing the LAG function
Modify the query to show confirmed for the day before.
```sql
  SELECT name, DAY(whn), confirmed,
  LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) FROM covid
    WHERE name = 'Italy' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
    ORDER BY whn
```
3. Number of new cases
Show the number of new cases for each day, for Italy, for March.
```sql
  SELECT name, DAY(whn),
  (confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn)) AS days FROM covid
    WHERE name = 'Italy' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
    ORDER BY whn
```
4. Weekly changes
Show the number of new cases in Italy for each week in 2020 - show Monday only.
```sql
  SELECT name, DATE_FORMAT(whn, '%Y-%m-%d') AS dates,
  (confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn)) AS weeks FROM covid
    WHERE name = 'Italy' AND WEEKDAY(whn) = 0 AND YEAR(whn) = 2020
    ORDER BY whn
```
5. LAG using a JOIN
Show the number of new cases in Italy for each week - show Monday only.
```sql
  SELECT tw.name, DATE_FORMAT(tw.whn, '%Y-%m-%d') AS dates,
  (tw.confirmed - lw.confirmed) AS weeks FROM covid tw
    LEFT JOIN covid lw ON DATE_ADD(lw.whn, INTERVAL 1 WEEK) = tw.whn AND tw.name = lw.name
    WHERE tw.name = 'Italy' AND (WEEKDAY(tw.whn) = 0)
    ORDER BY tw.whn
```
6. RANK()
Add a column to show the ranking for the number of deaths due to COVID.
```sql
  SELECT name, confirmed,
  RANK() OVER (ORDER BY confirmed DESC) AS rank_confirmed, deaths,
  RANK() OVER (ORDER BY deaths DESC) AS rank_deaths FROM covid
    WHERE whn = '2020-04-20'
    ORDER BY confirmed DESC
```
7. Infection rate
Show the infection rate ranking for each country. Only include countries with a population of at least 10 million.
```sql
  SELECT world.name, ROUND(100000 * confirmed / population, 2),
  RANK() OVER(ORDER BY 100000 * confirmed / population) AS rank FROM covid
    JOIN world ON covid.name = world.name
    WHERE whn = '2020-04-20' AND population > 10000000
    ORDER BY population DESC
```
8. Turning the corner
For each country that has had at last 1000 new cases in a single day, show the date of the peak number of new cases.
```sql
  WITH DailyCases AS (
      SELECT
          name, 
          whn, 
          (confirmed - LAG(confirmed)) OVER (PARTITION BY name ORDER BY whn) AS new_cases
      FROM covid
  ), PeakCases AS (
      SELECT 
          name, 
          whn, 
          new_cases,
          RANK() OVER (PARTITION BY name ORDER BY new_cases DESC) AS rank
      FROM DailyCases
      WHERE new_cases IS NOT NULL AND new_cases >= 1000
  )
  SELECT 
      name, 
      DATE_FORMAT(whn, '%Y-%m-%d') AS peakDate, 
      new_cases AS peakNewCases
  FROM PeakCases
    WHERE rank = 1
    ORDER BY peakDate
```