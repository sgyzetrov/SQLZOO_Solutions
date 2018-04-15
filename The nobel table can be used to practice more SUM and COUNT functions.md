## The nobel table can be used to practice more SUM and COUNT functions

Show the total number of prizes awarded.

```sql
SELECT COUNT(winner) FROM nobel
```

List each subject - just once

```sql
select distinct subject from nobel
```

Show the total number of prizes awarded for Physics.

```sql
select count(subject) from nobel where subject='Physics'
```

For each subject show the subject and the number of prizes.

```sql
select subject, count(subject) as number_of_prizes from nobel group by subject
```

For each subject show the first year that the prize was awarded.

```sql
select subject, min(yr) from nobel group by subject
```

For each subject show the number of prizes awarded in the year 2000.

```sql
select subject, count(subject) as number_of_prize from nobel where yr='2000' group by subject
```

Show the number of different winners for each subject.

```sql
select subject, count(distinct winner) from nobel group by subject
```

For each subject show how many years have had prizes awarded.

```sql
select subject, count(distinct yr) from nobel group by subject
```

Show the years in which three prizes were given for Physics.

```sql
select yr from nobel where subject='Physics' group by yr having count(subject)=3
```

Show winners who have won more than once.

```sql
select winner from nobel group by winner having count(winner)>1
```

Show winners who have won more than one subject.

```sql
select winner from nobel group by winner having count(distinct subject)>1
```

Show the year and subject where 3 prizes were given. Show only years 2000 onwards.

```sql
select yr, subject from nobel where yr >= 2000 group by yr, subject having count(subject)=3
```