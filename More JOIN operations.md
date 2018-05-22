## More JOIN operations

List the films where the yr is 1962 [Show id, title]

```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```

Give year of 'Citizen Kane'.

```sql
select yr from movie where title='Citizen Kane'
```

List all of the Star Trek movies, include the id, title AND yr (all of these movies include the words Star Trek in the title). Order results by year.

```sql
select id, title, yr from movie where title like '%Star Trek%' order by yr
```

What id number does the actor 'Glenn Close' have?

```sql
select id from actor where name='Glenn Close'
```

What is the id of the film 'Casablanca'

```sql
select id from movie where title='Casablanca'
```

Obtain the cast list for 'Casablanca'. Use movieid=11768, (or whatever value you got from the previous question)

```sql
select actor.name from casting join actor on casting.actorid=actor.id where casting.movieid=11768
```

Obtain the cast list for the film 'Alien'

```sql
select actor.name from 
(casting join movie on casting.movieid=movie.id) join actor on casting.actorid=actor.id 
where movie.title='Alien'
```

List the films in which 'Harrison Ford' has appeared

```sql
select movie.title from 
(casting join movie on casting.movieid=movie.id) join actor on casting.actorid=actor.id 
where actor.name='Harrison Ford'
```

List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]

```sql
select movie.title from 
(casting join movie on casting.movieid=movie.id) join actor on casting.actorid=actor.id 
where actor.name='Harrison Ford' AND casting.ord <> 1
```

List the films together with the leading star for all 1962 films.

```sql
select movie.title, actor.name from 
(casting join movie on casting.movieid=movie.id) join actor on casting.actorid=actor.id 
where movie.yr = 1962 AND casting.ord = 1
```

Which were the busiest years for 'John Travolta', show the year AND the number of movies he made each year for any year in which he made more than 2 movies.

```sql
SELECT yr,COUNT(title) FROM
movie JOIN casting ON movie.id=movieid JOIN actor ON actorid=actor.id
where name='John Travolta'
GROUP BY yr
HAVING COUNT(title)>2
```

List the film title and the leading actor for all of the films 'Julie Andrews' played in.

Title is not a unique field, create a table of IDs in your subquery

```sql
SELECT movie.title, actor.name FROM (
    casting JOIN movie ON movie.id=casting.movieid
    ) 
    JOIN actor ON casting.actorid=actor.id 
WHERE movie.id IN ( 
    SELECT movieid FROM 
    casting
    WHERE actorid IN (
        SELECT id FROM 
        actor
        WHERE name='Julie Andrews'
        )
    ) 
    AND casting.ord = 1

```

Obtain a list, in alphabetical order, of actors who've had at least 30 starring roles.

```sql
SELECT name
FROM actor
JOIN casting ON (id = actorid AND (
        SELECT COUNT(ord) FROM 
        casting 
        WHERE actorid = actor.id AND ord=1
        ) >= 30
    )
GROUP BY name
```

List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

```sql
select title, count(actorid) actor_num from movie join casting on movie.id=casting.movieid where yr=1978 group by title order by actor_num desc, title
```

List all the people who have worked with 'Art Garfunkel'.

```sql
select actor.name from (
    actor join casting on actor.id=casting.actorid
    ) 
    where movieid in (
        select movieid from (
            actor join casting on actor.id=casting.actorid
            ) 
            where actor.name='Art Garfunkel'
        ) and actorid not in (
            select id from 
            actor 
            where name='Art Garfunkel'
            )
```

## More JOIN Quiz

keys:

C, E, C, B, D, C, B