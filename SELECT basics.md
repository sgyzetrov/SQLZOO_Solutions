## SELECT basics

Modify it to show the population of Germany

```sql
SELECT population FROM world
  WHERE name = 'Germany'
```

Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

```sql
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway' , 'Denmark');
```

Just the right size

```sql
SELECT name, area FROM world
  WHERE area BETWEEN 200000 and 250000
```

## SELECT Quiz

key:

C, E, E, C, C, C, C 
