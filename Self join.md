## Self join

How many stops are in the database.

```sql
SELECT COUNT(id) FROM stops
```

Find the id value for the stop 'Craiglockhart'

```sql
SELECT id FROM stops WHERE name='Craiglockhart'
```

Give the id and the name for the stops on the '4' 'LRT' service.

```sql
SELECT id, name FROM stops JOIN route ON stops.id=route.stop WHERE num='4' AND company='LRT'
```

The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

```sql
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num HAVING COUNT(*)=2
```

Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop=149
```

The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'

```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name='London Road'
```

Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')

```sql
SELECT a.company, a.num FROM 
route AS a JOIN route AS b ON (a.company=b.company AND a.num=b.num) 
WHERE a.stop=115 AND b.stop=137 GROUP BY a.num, a.company
```

Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'

```sql
SELECT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name='Tollcross'
```

Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

```sql
SELECT stopa.name, a.company, a.num
FROM route a
  JOIN route b ON (a.num=b.num AND a.company=b.company)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopb.name = 'Craiglockhart' AND b.company='LRT'
```

Find the routes involving two buses that can go from Craiglockhart to Sighthill.
Show the bus no. and company for the first bus, the name of the stop for the transfer,
and the bus no. and company for the second bus.
Hint: Self-join twice to find buses that visit Craiglockhart and Sighthill, then join those on matching stops.

```sql
SELECT DISTINCT a.num, a.company, stopb.name ,  c.num,  c.company
FROM route a JOIN route b
ON (a.company = b.company AND a.num = b.num)
JOIN ( route c JOIN route d ON (c.company = d.company AND c.num= d.num))
JOIN stops stopa ON (a.stop = stopa.id)
JOIN stops stopb ON (b.stop = stopb.id)
JOIN stops stopc ON (c.stop = stopc.id)
JOIN stops stopd ON (d.stop = stopd.id)
WHERE  stopa.name = 'Craiglockhart' AND stopd.name = 'Sighthill'
            AND  stopb.name = stopc.name
ORDER BY LENGTH(a.num), b.num, stopb.id, LENGTH(c.num), d.num
```

## Self join Quiz

keys:

C, E, D