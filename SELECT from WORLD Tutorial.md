## SELECT from WORLD Tutorial

Observe the result of running this SQL command to show the name, continent and population of all countries.

```sql
SELECT name, continent, population FROM world
```

Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

```sql
SELECT name FROM world
WHERE population >= 200000000
```

Give the name and the per capita GDP for those countries with a population of at least 200 million.

per capita GDP is the GDP divided by the population GDP/population

```sql
select name, (GDP/population) pgdp from world where population >= 200000000
```

Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

```sql
  select name, (population/1000000) population_mills from world where continent = 'South America'
```

Show the countries which have a name that includes the word 'United'

```sql
select name from world where name like '%United%'
```

Show the countries that are big by area or big by population. Show name, population and area.

```sql
select name, population, area from world where area>= 3000000 or population>= 250000000
```

Exclusive OR (XOR). Show the countries that are big by area or big by population but not both. Show name, population and area.

```sql
select name, population, area from world where area>= 3000000 xor population>= 250000000
```

Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.

```sql
select name, round(population/1000000,2), round(gdp/1000000000,2) from world where continent='South America'
```

Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

```sql
select name, round(GDP/population,-3) from world where  GDP >= 1000000000000
```

Show the name and capital where the name and the capital have the same number of characters.

```sql
SELECT name, capital
  FROM world
 WHERE LENGTH(name) = LENGTH(capital)
```

Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

```sql
select name, capital from world where LEFT(name,1)=LEFT(capital,1) and name <> capital
```

Find the country that has all the vowels and no spaces in its name.

```sql
SELECT name
   FROM world
WHERE name not LIKE '% %'
  AND name LIKE '%a%' 
  AND name LIKE '%e%' 
  AND name LIKE '%i%' 
  AND name LIKE '%o%' 
  AND name LIKE '%u%'
```

## BBC QUIZ

key:

E, D, B, D, B, D, C