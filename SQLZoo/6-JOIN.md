# SQLZoo
There are queries for section 6 from website [SQLZoo](https://www.sqlzoo.net/wiki/The_JOIN_operation).

## JOIN

1. 
Modify querie to show the matchid and player name for all goals scored by Germany.
```sql
  SELECT matchid, player FROM goal 
    WHERE teamid = 'GER'
```
2. 
Show id, stadium, team1, team2 for just game 1012.
```sql
  SELECT id, stadium, team1, team2 FROM game
    WHERE id = 1012
```
3. 
Modify querie to show the player, teamid, stadium and mdate for every German goal.
```sql
  SELECT player, teamid, stadium, mdate FROM game
    JOIN goal ON id = matchid
    WHERE teamid = 'GER'
```
4. 
Show the team1, team2 and player for every goal scored by a player called Mario.
```sql
  SELECT team1, team2, player FROM game
    JOIN goal ON id = matchid
    WHERE player LIKE 'Mario%'
```
5. 
Show player, teamid, coach, gtime for all goals scored in the first 10 minutes.
```sql
  SELECT player, teamid, coach, gtime FROM goal
    JOIN eteam on teamid = id
    WHERE gtime <= 10
 ```
6. 
List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
```sql
  SELECT mdate, teamname FROM game
    JOIN eteam ON team1 = eteam.id
    WHERE coach = 'Fernando Santos'
```
7. 
List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'.
```sql
  SELECT player FROM goal
    JOIN game ON matchid = id
    WHERE stadium = 'National Stadium, Warsaw'
```
### More difficult questions
8. 
Show the name of all players who scored a goal against Germany.
```sql
  SELECT DISTINCT player FROM game
    JOIN goal ON matchid = id 
    WHERE ( team1 = 'GER' OR team2 = 'GER' ) AND teamid <> 'GER'
```
9. 
Show teamname and the total number of goals scored.
```sql
  SELECT teamname, COUNT(gtime) AS Total FROM eteam
    JOIN goal ON id = teamid
    GROUP BY teamname
```
10. 
Show the stadium and the number of goals scored in each stadium.
```sql
  SELECT stadium, COUNT(gtime) AS Total FROM game
    JOIN goal ON matchid = id
    GROUP BY stadium
```
11. 
For every match involving 'POL', show the matchid, date and the number of goals scored.
```sql
  SELECT matchid, mdate, COUNT(gtime) FROM game
    JOIN goal ON matchid = id
    WHERE ( team1 = 'POL' OR team2 = 'POL' )
    GROUP BY mdate, matchid
    ORDER BY matchid ASC
```
12. 
For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
```sql
  SELECT matchid, mdate, COUNT(gtime) FROM goal
    JOIN game ON matchid = id
    WHERE teamid = 'GER'
    GROUP BY matchid, mdate
```
13. 
List every match with the goals scored by each team as shown.
```sql
  SELECT DISTINCT mdate, team1,
	SUM( CASE WHEN teamid = team1 THEN 1 ELSE 0 END ) score1, team2,
  SUM( CASE WHEN teamid = team2 THEN 1 ELSE 0 END ) score2 FROM game
    LEFT JOIN goal ON game.id = goal.matchid
    GROUP BY id, mdate, team1, team2
    ORDER BY mdate, matchid, team1, team2
```