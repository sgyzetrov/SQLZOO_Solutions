## SUM and COUNT

Show the total population of the world.

```sql
SELECT SUM(population)
FROM world
```

List all the continents - just once each.

```sql
select distinct continent from world
```

Give the total GDP of Africa

```sql
select sum(gdp) from world where continent='Africa'
```

How many countries have an area of at least 1000000

```sql
select count(name) from world where area>=1000000
```

What is the total population of ('Estonia', 'Latvia', 'Lithuania')

```sql
select sum(population) from world where name in ('Estonia', 'Latvia', 'Lithuania')
```

For each continent show the continent and number of countries.

```sql
select continent, count(name) from world group by continent
```

For each continent show the continent and number of countries with populations of at least 10 million.

```sql
select continent, count(name) from world x where x.population>=10000000 group by continent
```

List the continents that have a total population of at least 100 million.

```sql
SELECT continent
  FROM world
 GROUP BY continent
HAVING SUM(population)>100000000
```

## SUM and COUNT Quiz

keys:

C, A, D, E, B, E, D, D

