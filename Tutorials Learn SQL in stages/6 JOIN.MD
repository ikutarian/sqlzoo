## 1. Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'

```SQL
SELECT matchid, player FROM goal WHERE teamid = 'GER'
```

## 2. Show id, stadium, team1, team2 for just game 1012

```SQL
SELECT id,stadium,team1,team2 FROM game WHERE id = 1012
```

## 3. Modify it to show the player, teamid, stadium and mdate and for every German goal.

```SQL
SELECT player,teamid, stadium, mdate 
FROM game JOIN goal ON (id=matchid) WHERE teamid = 'GER'
```

## 4. Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'

```SQL
SELECT team1, team2, player FROM game JOIN goal ON (id = matchid) WHERE player LIKE 'Mario%'
```

## 5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10

```SQL
SELECT player, teamid, coach, gtime 
FROM goal JOIN eteam ON teamid = id WHERE gtime<=10
```

## 6. List the the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

```SQL
SELECT mdate, teamname FROM game JOIN eteam ON (team1=eteam.id) WHERE coach = 'Fernando Santos'
```

## 7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'

```SQL
SELECT player FROM game JOIN goal ON (id = matchid) WHERE stadium = 'National Stadium, Warsaw'
```

## 8. Instead show the name of all players who scored a goal against Germany.

```SQL
SELECT DISTINCT player 
FROM game JOIN goal ON matchid = id WHERE teamid != 'GER' AND (team1 = 'GER' OR team2 = 'GER')
```

## 9. Show teamname and the total number of goals scored.

```SQL
SELECT teamname, COUNT(*) FROM eteam JOIN goal ON id = teamid GROUP BY teamname
```

## 10. Show the stadium and the number of goals scored in each stadium.

```SQL
SELECT stadium, COUNT(*) FROM game JOIN goal ON (id = matchid) GROUP BY stadium 
```

## 11. For every match involving 'POL', show the matchid, date and the number of goals scored.

```SQL
SELECT t.matchid, t.mdate, count(t.matchid) AS goals
FROM
  (SELECT matchid, mdate 
   FROM game JOIN goal ON (id = matchid)
   WHERE team1 = 'POL' OR team2 = 'POL') AS t
GROUP BY t.matchid
```

## 12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'

```SQL
SELECT t.matchid, t.mdate, count(t.matchid) AS goals
FROM
  (SELECT matchid, mdate 
   FROM game JOIN goal ON (id = matchid)
   WHERE teamid = 'GER') AS t
GROUP BY t.matchid
```

## 13. List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.

```SQL
```