# SQLZoo Solutions
Documenting my [SQLZoo](https://sqlzoo.net/wiki/SQL_Tutorial) solutions.

## Sections
0. [SELECT basics](#select-basics)
1. [SELECT name](#select-name)
2. [SELECT from World](#select-from-world)
3. [SELECT from Nobel](#select-from-nobel)
4. [SELECT within SELECT](#select-within-select)
5. [SUM and Count](#sum-and-count)
6. [JOIN](#join)
7. [More JOIN operations](#more-join-operations)
8. [Using Null](#using-null)
9. [Numeric Examples](#numeric-examples)
10. [Window function](#window-function)
11. [COVID 19](#covid-19)
12. [Self join](#self-join)
13. [Tutorial Quizzes](#tutorial-quizzews)
14. [Tutorial Student Records](#tutorial-student-records)
15. [Tutorial DDL](#tutorial-ddl)

## SELECT basics
### 1.
```sql
SELECT population 
FROM world
WHERE name = 'Germany'
```
### 2.
```sql
SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```
### 3.
```sql
SELECT name, area
FROM world
WHERE area BETWEEN 200000 AND 250000
```

## SELECT name
### 1.
```sql
SELECT name
FROM world
WHERE name LIKE 'Y%'
```
### 2.
```sql
SELECT name
FROM world
WHERE name LIKE '%y'
```
### 3.
```sql
SELECT name
FROM world
WHERE name LIKE '%x%'
```
### 4.
```sql
SELECT name
FROM world
WHERE name LIKE '%land'
```
### 5.
```sql
SELECT name
FROM world
WHERE name LIKE 'C%' AND name LIKE '%ia'
```
### 6.
```sql
SELECT name
FROM world
WHERE name LIKE '%oo%'
```
### 7.
```sql
SELECT name
FROM world
WHERE name LIKE '%a%a%a%'
```
### 8.
```sql
SELECT name FROM world
WHERE name LIKE '_t%'
ORDER BY name
```
### 9.
```sql
SELECT name
FROM world
WHERE name LIKE '%o__o%'
```
### 10.
```sql
SELECT name
FROM world
WHERE name LIKE '____'
```
### 11.
```sql
SELECT name
FROM world
WHERE name = capital;
```
### 12.
```sql
SELECT name
FROM world
WHERE capital = CONCAT(name, ' City')
```
### 13.
```sql
SELECT capital, name
FROM world
WHERE capital LIKE CONCAT('%', name, '%')
```
### 14.
```sql
SELECT capital, name
FROM world
WHERE capital LIKE CONCAT('%', name, '_%')
```
### 15.
```sql
SELECT name, REPLACE(capital, name, '')
FROM world
WHERE capital LIKE CONCAT('%', name, '_%')
```

## SELECT from World
### 1.
```sql
SELECT name, continent, population
FROM world
```
### 2.
```sql
SELECT name
FROM world
WHERE population >= 200000000
```
### 3.
```sql
SELECT name
FROM world
WHERE population >= 200000000
```
### 4.
```sql
SELECT name, population/1000000 as 'Population per Million'
FROM world
WHERE continent = 'South America'
```
### 5.
```sql
SELECT name, population
FROM world
WHERE name in ('France', 'Germany', 'Italy')
```
### 6.
```sql
SELECT name
FROM world
WHERE name LIKE '%United%'
```
### 7.
```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 OR population > 250000000
```
### 8.
```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000 AND population <= 250000000) OR (area <= 3000000 AND population > 250000000)
```
### 9.
```sql
SELECT name, ROUND(population/1000000, 2) AS 'population_in_millions', ROUND(GDP/1000000000,2) AS 'GDP_in_billions'
FROM world
WHERE continent = 'South America'
```
### 10.
```sql
SELECT name, ROUND(GDP/population, -3) AS 'GDP_per_capita'
FROM world
WHERE GDP >= 1000000000000 
```
### 11.
```sql
SELECT name, capital  
FROM world
WHERE LENGTH(name) = LENGTH(capital)
```
### 12.
```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name != capital
```
### 13.
```sql
SELECT name
FROM world
WHERE name LIKE '%a%'
  AND name LIKE '%e%'
  AND name LIKE '%i%'
  AND name LIKE '%o%'
  AND name LIKE '%u%'
  AND name NOT LIKE '% %'
```

## SELECT from Nobel
### 1.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950
```
### 2.
```sql
SELECT winner
FROM nobel
WHERE yr = 1962 AND subject = 'literature'
```
### 3.
```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```
### 4.
```sql
SELECT winner
FROM nobel
WHERE subject = 'peace' AND yr >= 2000
```
### 5.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'literature' AND yr BETWEEN 1980 AND 1989
```
### 6.
```sql
SELECT * 
FROM nobel
WHERE winner in ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter', 'Barack Obama')
```
### 7.
```sql
SELECT winner
FROM nobel
WHERE winner like 'John%'
```
### 8.
```sql
SELECT *
FROM nobel
WHERE (subject = 'physics' AND yr = 1980) OR (subject = 'chemistry' AND yr = 1984)
```
### 9.
```sql
SELECT *
FROM nobel
WHERE yr = 1980 AND subject NOT IN ('chemistry', 'medicine')
```
### 10.
```sql
SELECT *
FROM nobel
WHERE (subject = 'Medicine' AND yr < 1910) OR (subject = 'Literature' AND yr >= 2004)
```
### 11.
```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG'
```
### 12.
```sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O''NEILL'
```
### 13.
```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner like 'Sir%'
ORDER BY yr DESC, winner
```

