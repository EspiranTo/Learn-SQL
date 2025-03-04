There are queries for section 9 from website [SQLZoo](https://sqlzoo.net/wiki/Self_join).

## Self join

### Summary
1. 
How many stops are in the database.
```sql
  SELECT COUNT(id) FROM stops
```
2. 
Find the id value for the stop 'Craiglockhart'.
```sql
  SELECT id FROM stops
    WHERE name = 'Craiglockhart'
```
3. 
Give the id and the name for the stops on the '4' 'LRT' service.
```sql
  SELECT stops.id, stops.name FROM stops
    JOIN route ON stops.id = route.stop
    WHERE num = '4' AND company = 'LRT'
```
### Routes and stops
4. 
The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53).
Run the query and notice the two services that link these stops have a count of 2.
Add a HAVING clause to restrict the output to these two routes.
```sql
  SELECT company, num, COUNT(*) FROM route
    WHERE stop IN (149, 53)
    GROUP BY num, company
    HAVING COUNT(stop) = 2
```
5. 
Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes.
Change the query so that it shows the services from Craiglockhart to London Road.
```sql
  SELECT a.company, a.num, a.stop, b.stop FROM route a
    JOIN route b ON a.num = b.num AND a.company = b.company
    WHERE a.stop = 53 AND b.stop = 149
```
6. 
The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number.
Change the query so that the services between 'Craiglockhart' and 'London Road' are shown.
If you are tired of these places try 'Fairmilehead' against 'Tollcross'.
```sql
  SELECT a.company, a.num, s1.name, s2.name FROM route a
    JOIN route b ON a.num = b.num AND a.company = b.company
    JOIN stops s1 ON a.stop = s1.id
    JOIN stops s2 ON b.stop = s2.id
    WHERE s1.name = 'Craiglockhart' AND s2.name = 'London Road'
```
### Using a self join
7. 
Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith').
```sql
  SELECT DISTINCT a.company, a.num FROM route a
    JOIN route b ON a.num = b.num AND a.company = b.company
    WHERE a.stop = 115 AND b.stop = 137
```
8. 
Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'.
```sql
  SELECT a.company, a.num FROM route a
    JOIN route b ON a.num = b.num AND a.company = b.company
    JOIN stops s1 ON a.stop = s1.id
    JOIN stops s2 ON b.stop = s2.id
    WHERE s1.name = 'Craiglockhart' AND s2.name = 'Tollcross'
```
9. 
Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company.
Include the company and bus no. of the relevant services.
```sql
  SELECT stops.name, route.company, route.num FROM route
    JOIN stops ON route.stop = stops.id
    WHERE route.company = 'LRT'
    AND route.num IN
      ( SELECT num FROM route WHERE stop =
        ( SELECT id FROM stops WHERE name = 'Craiglockhart' ))
```
10. 
Find the routes involving two buses that can go from Craiglockhart to Lochend.
Show the bus no. and company for the first bus, the name of the stop for the transfer, and the bus no. and company for the second bus.
```sql
  SELECT
    r1.num AS bus1_num,
    r1.company AS bus1_company,
    s.name AS transfer_stop,
    r4.num AS bus2_num,
    r4.company AS bus2_company
  FROM route r1, route r2, stops s, route r3, route r4
  WHERE
    r1.num = r2.num AND
    r1.company = r2.company AND
    r2.stop = s.id AND
    s.id = r3.stop AND
    r3.num = r4.num AND
    r3.company = r4.company AND
    r1.stop = ( SELECT id FROM stops WHERE name = 'Craiglockhart' ) AND
    r4.stop = ( SELECT id FROM stops WHERE name = 'Lochend' )
  ORDER BY r1.num, s.name, r4.num
```