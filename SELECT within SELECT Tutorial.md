## SELECT within SELECT Tutorial

List each country name where the population is larger than that of 'Russia'.

```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```

Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

```sql
select name from world where continent = 'Europe' and ((gdp/population) > (select gdp/population from world where name='United Kingdom'))
```

List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

```sql
select name, continent from world where continent in (select continent from world where name='Argentina' or name = 'Australia') order by name
```

Which country has a population that is more than Canada but less than Poland? Show the name and the population.

```sql
select name, population from world where population >(select population from world where name='Canada') and population < (select population from world where name='Poland')
```

Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

```sql
select name, concat(round((population/(select population from world where name='Germany'))*100,0),'%') from world where continent='Europe'
```

Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)

```sql
select name from world where gdp > all(select gdp from world where continent = 'Europe' and gdp>0)
-- Some countries may have NULL gdp values, so need `gdp>0`
```

Find the largest country (by area) in each continent, show the continent, the name and the area:

```sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent)
```

List each continent and the name of the country that comes first alphabetically.

```sql
select continent, name from world x where name=(select name from world y where x.continent = y.continent limit 1)
```

Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

```sql
SELECT name, continent, population
FROM world x
WHERE 25000000  > ALL(SELECT population FROM world y WHERE x.continent = y.continent AND y.population > 0)
```

Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.

```sql
select name, continent from world x
where x.population > all(select 3*population from world y where x.continent = y.continent and y.population > 0 and x.name <> y.name)
```

## Nested SELECT Quiz

keys:

C, B, A, D, B, B, B