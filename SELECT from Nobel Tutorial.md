## SELECT from Nobel Tutorial

Change the query shown so that it displays Nobel prizes for 1950.

```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

Show who won the 1962 prize for Literature.

```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```

Show the year and subject that won 'Albert Einstein' his prize.

```sql
select yr, subject from nobel where winner = 'Albert Einstein'
```

Give the name of the 'Peace' winners since the year 2000, including 2000.

```sql
select winner from nobel where subject = 'Peace' and yr>=2000
```

Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive.

```sql
select yr, subject, winner from nobel where subject='Literature' and yr >=1980 and yr <=1989
```

Show all details of the presidential winners:

- Theodore Roosevelt
- Woodrow Wilson
- Jimmy Carter
- Barack Obama

```sql
SELECT * FROM nobel
WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter',
                  'Barack Obama')
```

Show the winners with first name John

```sql
select winner from nobel where winner like 'John %'
```

Show the Physics winners for 1980 together with the Chemistry winners for 1984.

```sql
select yr, subject, winner from nobel where (yr=1980 and subject='Physics') or (yr=1984 and subject='Chemistry')
```

Show the winners for 1980 excluding the Chemistry and Medicine

```sql
select yr, subject, winner from nobel where subject not in ('Chemistry', 'Medicine') and yr=1980
```

Show who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)

```sql
select yr, subject, winner from nobel where (subject='Medicine' and yr<1910) or (subject='Literature' and yr >= 2004)
```

Find all details of the prize won by PETER GRÜNBERG

```sql
select * from nobel where winner='PETER GRÜNBERG'
```

Find all details of the prize won by EUGENE O'NEILL

```sql
select * from nobel where winner = 'EUGENE O\'NEILL'
```

List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.

```sql
select winner, yr, subject from nobel where winner like 'Sir %' order by yr desc, winner
```

Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('Physics','Chemistry'),subject,winner
```

## Nobel Quiz

keys:

E, C, B, C, C, C, D