## The JOIN operation

show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'

```sql
SELECT matchid, player FROM goal 
  WHERE teamid='GER'
```

Show id, stadium, team1, team2 for just game 1012

```sql
SELECT id,stadium,team1,team2
  FROM game
where id=1012
```

show the player, teamid, stadium and mdate and for every German goal.

```sql
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid)
  WHERE teamid='GER'
```

Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'

```sql
select team1, team2, player from game join goal on (game.id=goal.matchid)
where player like 'Mario%'
```

Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10

```sql
SELECT player, teamid, coach, gtime
  FROM goal join eteam on goal.teamid=eteam.id
 WHERE gtime<=10
```

List the the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

```sql
select mdate, teamname from game join eteam on (game.team1=eteam.id) where coach='Fernando Santos'
```

List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'

```sql
select player from game join goal on (game.id=goal.matchid) where stadium='National Stadium, Warsaw'
```

show the name of all players who scored a goal against Germany.

```sql
SELECT DISTINCT(player)
FROM game JOIN goal ON goal.matchid = game.id
WHERE ((team1='GER' OR team2='GER') AND teamid <> 'GER')
```

Show teamname and the total number of goals scored.

```sql
SELECT teamname, count(gtime)
  FROM eteam JOIN goal ON eteam.id=goal.teamid
GROUP BY teamname
```

Show the stadium and the number of goals scored in each stadium.

```sql
select stadium, count(gtime) from game join goal on (game.id=goal.matchid) group by stadium
```

For every match involving 'POL', show the matchid, date and the number of goals scored.

```sql
SELECT matchid,mdate, count(gtime)
  FROM game JOIN goal ON goal.matchid = game.id 
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid,mdate
```

For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'

```sql
SELECT matchid,mdate, count(gtime)
  FROM game JOIN goal ON goal.matchid = game.id 
 WHERE teamid='GER'
GROUP BY matchid,mdate
```

List every match with the goals scored by each team as shown.

```sql
SELECT mdate,
       team1,
       SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) AS score1,
       team2,
       SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score2 
FROM game LEFT JOIN goal ON (id = matchid)
    GROUP BY mdate,team1,team2
    ORDER BY mdate, matchid, team1, team2
```

## Old JOIN Tutorial

Show the athelete (who) and the country name for medal winners in 2000.

```sql
SELECT who, country.name
  FROM ttms JOIN country
         ON (ttms.country=country.id)
 WHERE games = 2000
```

Show the who and the color of the medal for the medal winners from 'Sweden'.

```sql
select who, color   
FROM ttms JOIN country
         ON (ttms.country=country.id)
WHERE country='SWE'
```

Show the years in which 'China' won a 'gold' medal.

```sql
select games from ttms join country ON (ttms.country=country.id)
where country='CHN' and color='gold'
```

Show who won medals in the 'Barcelona' games.

```sql
SELECT who
  FROM ttws JOIN games
            ON (ttws.games=games.yr)
  WHERE city = 'Barcelona'
```

Show which city 'Jing Chen' won medals. Show the city and the medal color.

```sql
select city, color
from ttws join games on (ttws.games=games.yr)
where who= 'Jing Chen'
```

Show who won the gold medal and the city.

```sql
select who, city
from ttws join games on (ttws.games=games.yr)
where color= 'gold'
```

Show the games and color of the medal won by the team that includes 'Yan Sen'.

```sql
select games, color
from ttmd join team on ttmd.team=team.id
where team.name='Yan Sen'
```

Show the 'gold' medal winners in 2004.

```sql
select team.name
from ttmd join team on ttmd.team=team.id
where ttmd.color='Gold' and ttmd.games=2004
```

Show the name of each medal winner country 'FRA'.

```sql
select team.name
from ttmd join team on ttmd.team=team.id
where country='FRA'
```

## JOIN Quiz

keys:

D, C, A, A, B, C, B
