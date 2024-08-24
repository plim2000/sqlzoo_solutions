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

## SELECT within SELECT
### 1.
```sql
SELECT name 
FROM world
WHERE population >
  (SELECT population 
  FROM world
  WHERE name='Russia')
```
### 2.
```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND GDP/population > (SELECT GDP/POPULATION
                                                 FROM world
                                                 WHERE name = 'United Kingdom')
```
### 3.
```sql
SELECT name, continent
FROM world
WHERE continent IN (SELECT DISTINCT continent FROM world WHERE name in ('Argentina','Australia'))
ORDER BY name
```
### 4.
```sql
SELECT name, population
FROM world
WHERE population > (SELECT population FROM world WHERE name = 'United Kingdom')
  AND population < (SELECT population FROM world WHERE name = 'Germany')
```
### 5.
```sql
SELECT name, CONCAT(ROUND(population/(SELECT population FROM world WHERE name = 'Germany')*100,0),'%') AS percentage
FROM world
WHERE continent = 'Europe'
```
### 6.
```sql
SELECT name
FROM world
WHERE gdp > ALL(SELECT gdp FROM world WHERE CONTINENT = 'Europe' AND gdp >= 0)
```
### 7.
```sql
SELECT continent, name, area
FROM world t1
WHERE area = (SELECT MAX(area)
              FROM world t2
              WHERE t1.continent = t2.continent)
```
### 8.
```sql
SELECT w1.continent, w1.name
FROM world w1
WHERE name = (SELECT MIN(w2.name)
              FROM world w2
              WHERE w1.continent = w2.continent)
```
### 9.
```sql
SELECT name, continent, population 
FROM world w1
WHERE 25000000 >= ALL(SELECT population
                      FROM world w2
                      WHERE w1.continent = w2.continent)
```
### 10.
```sql
SELECT name, continent
FROM world w1
WHERE population >= ALL(SELECT 3 * population
                        FROM world w2
                        WHERE w1.continent = w2.continent AND w1.name != w2.name)
```

## SUM and COUNT
### 1.
```sql
SELECT SUM(population)
FROM world
```
### 2.
```sql
SELECT DISTINCT continent
FROM world
```
### 3.
```sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa'
```
### 4.
```sql
SELECT COUNT(name)
FROM world
WHERE area >= 1000000
```
### 5.
```sql
SELECT sum(population)
FROM world
WHERE name in ('Estonia', 'Latvia', 'Lithuania')
```
### 6.
```sql
SELECT continent, COUNT(name)
FROM world
GROUP BY continent
```
### 7.
```sql
SELECT continent, COUNT(name)
FROM world
WHERE population > 10000000
GROUP BY continent
```
### 8.
```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) > 100000000
```

## JOIN
### 1.
```sql
SELECT matchid, player
FROM goal 
WHERE teamid = 'GER'
```
### 2.
```sql
SELECT id,stadium,team1,team2
FROM game
WHERE id = 1012
```
### 3.
```sql
SELECT goal.player, goal.teamid, game.stadium, game.mdate
FROM game JOIN goal ON (game.id = goal.matchid)
WHERE goal.teamid = 'GER'
```
### 4.
```sql
SELECT game.team1, game.team2, goal.player
FROM game JOIN goal ON (game.id = goal.matchid)
WHERE goal.player LIKE 'Mario%'
```
### 5.
```sql
SELECT goal.player, goal.teamid, eteam.coach, goal.gtime
FROM goal JOIN eteam ON (goal.teamid = eteam.id)
WHERE goal.gtime <= 10
```
### 6.
```sql
SELECT game.mdate, eteam.teamname
FROM game JOIN eteam ON (game.team1 = eteam.id)
WHERE eteam.coach = 'Fernando Santos'
```
### 7.
```sql
SELECT goal.player
FROM goal JOIN game ON (goal.matchid = game.id)
WHERE game.stadium = 'National Stadium, Warsaw'
```
### 8.
```sql
SELECT DISTINCT(goal.player)
FROM game JOIN goal ON (game.id = goal.matchid)
WHERE goal.teamid != 'GER' AND (game.team1 = 'GER' OR game.team2 = 'GER')
```
### 9.
```sql
SELECT eteam.teamname, COUNT(goal.player)
FROM eteam JOIN goal ON eteam.id = goal.teamid
GROUP BY eteam.teamname
```
### 10.
```sql
SELECT game.stadium, COUNT(goal.player) total_goals
FROM game JOIN goal ON (game.id = goal.matchid)
GROUP BY game.stadium
```
### 11.
```sql
SELECT goal.matchid, game.mdate, COUNT(*) total_goals
FROM game JOIN goal ON game.id = goal.matchid 
WHERE game.team1 = 'POL' OR game.team2 = 'POL'
GROUP BY goal.matchid, game.mdate
```
### 12.
```sql
SELECT goal.matchid, game.mdate, COUNT(*) total_goals
FROM goal JOIN game ON (goal.matchid = game.id)
WHERE goal.teamid = 'GER'
GROUP BY goal.matchid, game.mdate
```
### 13.
```sql
SELECT game.mdate, 
  game.team1, 
  SUM(CASE WHEN goal.teamid=game.team1 THEN 1 ELSE 0 END) score1,
  game.team2,
  SUM(CASE WHEN goal.teamid=game.team2 THEN 1 ELSE 0 END) score2
FROM game LEFT JOIN goal ON game.id = goal.matchid
GROUP BY game.mdate, game.team1, game.team2
ORDER BY game.mdate, goal.matchid, game.team1, game.team2
```

## More JOIN Operations
### 1.
```sql
SELECT id, title
FROM movie
WHERE yr = 1962
```
### 2.
```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane'
```
### 3.
```sql
SELECT id, title, yr
FROM movie
WHERE title like '%Star Trek%'
ORDER BY yr
```
### 4.
```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```
### 5.
```sql
SELECT id
FROM movie
WHERE title = 'Casablanca'
```
### 6.
```sql
SELECT actor.name
FROM movie JOIN casting ON movie.id = casting.movieid 
           JOIN actor ON casting.actorid = actor.id
WHERE casting.movieid = 11768
```
### 7.
```sql
SELECT actor.name
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE movie.title = 'Alien'
```
### 8.
```sql
SELECT movie.title
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE actor.name = 'Harrison Ford'
```
### 9.
```sql
SELECT movie.title
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE actor.name = 'Harrison Ford' AND casting.ord != 1
```
### 10.
```sql
SELECT movie.title, actor.name
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE movie.yr = 1962 AND casting.ord = 1
```
### 11.
```sql
SELECT movie.yr, COUNT(*) movie_count
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE actor.name = 'Rock Hudson'
GROUP BY movie.yr
HAVING COUNT(*) > 2
```
### 12.
```sql
SELECT movie.title, actor.name
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE casting.ord = 1 AND movie.id in (SELECT casting.movieid
                                         FROM casting JOIN actor ON casting.actorid = actor.id
                                         WHERE actor.name = 'Julie Andrews')
```
### 13.
```sql
SELECT subquery.name
FROM (SELECT actor.name, count(*) starring_role_count
      FROM movie JOIN casting ON movie.id = casting.movieid
                 JOIN actor ON casting.actorid = actor.id
      WHERE casting.ord = 1
      GROUP BY actor.name) subquery
WHERE subquery.starring_role_count >= 15
ORDER BY subquery.name
```
### 14.
```sql
SELECT movie.title, count(*) cast_count
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE movie.yr = 1978
GROUP BY movie.title
ORDER BY cast_count DESC, movie.title
```
### 15.
```sql
SELECT actor.name
FROM movie JOIN casting ON movie.id = casting.movieid
           JOIN actor ON casting.actorid = actor.id
WHERE movie.id IN (SELECT movie.id
                   FROM movie JOIN casting ON movie.id = casting.movieid
                              JOIN actor ON casting.actorid = actor.id
                   WHERE actor.name = 'Art Garfunkel') 
               AND actor.name != 'Art Garfunkel'
```

## Using NULL
### 1.
```sql
SELECT t.name
FROM teacher t LEFT JOIN dept d ON (t.dept = d.id)
WHERE t.dept is NULL
```
### 2.
```sql
SELECT teacher.name, dept.name
FROM teacher INNER JOIN dept ON (teacher.dept=dept.id)
```
### 3.
```sql
SELECT t.name, d.name
FROM teacher t LEFT JOIN dept d ON (t.dept = d.id)
```
### 4.
```sql
SELECT t.name, d.name
FROM teacher t RIGHT JOIN dept d ON (t.dept = d.id)
```
### 5.
```sql
SELECT t.name, COALESCE(t.mobile,  '07986 444 2266')
FROM teacher t LEFT JOIN dept d ON (t.dept = d.id)
```
### 6.
```sql
SELECT t.name, COALESCE(d.name, 'None')
FROM teacher t LEFT JOIN dept d ON (t.dept = d.id)
```
### 7.
```sql
SELECT COUNT(DISTINCT(name)) teacher_count, COUNT(DISTINCT(mobile)) phone_count
FROM teacher
```
### 8.
```sql
SELECT d.name, COUNT(t.name)
FROM teacher t RIGHT JOIN dept d ON (t.dept = d.id)
GROUP BY d.name
```
### 9.
```sql
SELECT name, (CASE WHEN dept in (1,2) THEN 'Sci' ELSE 'Art' END) as new_dept
FROM teacher
```
### 10.
```sql
SELECT name, (CASE WHEN dept in (1,2) THEN 'Sci' WHEN dept = 3 THEN 'ART' ELSE 'None' END) new_dept
FROM teacher
```

## Numeric Examples
### 1.
```sql
SELECT A_STRONGLY_AGREE
FROM nss
WHERE question='Q01'
    AND institution='Edinburgh Napier University'
    AND subject='(8) Computer Science'
```
### 2.
```sql
SELECT institution, subject
FROM nss
WHERE question='Q15' AND score >= 100
```
### 3.
```sql
SELECT institution, score
FROM nss
WHERE question='Q15'
    AND subject='(8) Computer Science'
    AND score < 50
```
### 4.
```sql
SELECT subject, SUM(response)
FROM nss
WHERE question='Q22'
    AND (subject='(8) Computer Science' 
    OR subject='(H) Creative Arts and Design')
GROUP BY subject
```
### 5.
```sql
SELECT subject, SUM(A_STRONGLY_AGREE/100*response)
FROM nss
WHERE question='Q22'
    AND (subject='(H) Creative Arts and Design' OR subject='(8) Computer Science')
GROUP BY subject
```
### 6.
```sql
SELECT subject, ROUND(SUM(A_STRONGLY_AGREE/100*response) / SUM(response)*100,0)
FROM nss
WHERE question='Q22'
    AND (subject='(H) Creative Arts and Design' OR subject='(8) Computer Science')
GROUP BY subject
```
### 7.
```sql
SELECT institution, round(sum(score*response)/sum(response),0)
FROM nss
WHERE question='Q22'
    AND institution LIKE '%Manchester%'
GROUP BY institution
```
### 8.
```sql
SELECT institution, 
    SUM(sample) total_sample, 
    SUM(CASE WHEN subject = '(8) Computer Science' THEN sample ELSE 0 END) comp_sci_sample
FROM nss
WHERE question='Q01' AND institution LIKE '%Manchester%'
GROUP BY institution
```

## Window function
### 1.
```sql
SELECT lastName, party, votes
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY votes DESC
```
### 2.
```sql
SELECT party, votes,
    RANK() OVER (ORDER BY votes DESC) as posn
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party
```
### 3.
```sql
SELECT yr,party, votes,
    RANK() OVER (PARTITION BY yr ORDER BY votes DESC) as posn
FROM ge
WHERE constituency = 'S14000021'
ORDER BY party,yr
```
### 4.
```sql
SELECT constituency,party, votes,
    RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) posn
FROM ge
WHERE (constituency BETWEEN 'S14000021' AND 'S14000026') AND (yr  = 2017)
ORDER BY posn, constituency
```
### 5.
```sql
WITH new_table AS (
    SELECT yr, constituency, party, votes,
        RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) posn
    FROM ge
    WHERE (constituency BETWEEN 'S14000021' AND 'S14000026') AND (yr  = 2017))


SELECT constituency, party
FROM new_table
WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
    AND yr = 2017
    AND posn = 1
```
### 6.
```sql
WITH rank_table AS (
    SELECT *, rank() OVER (PARTITION BY constituency ORDER BY votes DESC) posn
    FROM ge
    WHERE (constituency LIKE 'S%') AND (yr  = 2017))
  
SELECT party, COUNT(*) seats
FROM rank_table
WHERE posn = 1
GROUP BY party
```

## COVID 19
### 1.
```sql
SELECT name, DAY(whn), confirmed, deaths, recovered
FROM covid
WHERE name = 'Spain' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
### 2.
```sql
SELECT name, DAY(whn) day, confirmed,
    LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) dbf
FROM covid
WHERE name = 'Italy' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
### 3.
```sql
SELECT name, DAY(whn), 
   confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) new
FROM covid
WHERE name = 'Italy'
AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
### 4.
```sql
SELECT name, DATE_FORMAT(whn,'%Y-%m-%d'), confirmed
     - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) new_this_week
FROM covid
WHERE name = 'Italy' AND WEEKDAY(whn) = 0 AND YEAR(whn) = 2020
ORDER BY whn
```
### 5.
```sql
SELECT tw.name, DATE_FORMAT(tw.whn,'%Y-%m-%d'), tw.confirmed-lw.confirmed new_this_week
FROM covid tw LEFT JOIN covid lw ON (DATE_ADD(lw.whn, INTERVAL 1 WEEK) = tw.whn)
    AND (tw.name=lw.name)
WHERE tw.name = 'Italy' AND WEEKDAY(tw.whn) = 0
ORDER BY tw.whn
```
### 6.
```sql
SELECT 
    name, 
    confirmed,
    RANK() OVER (ORDER BY confirmed DESC) rc,
    deaths,
    RANK() OVER (ORDER BY deaths DESC) rd
FROM covid
WHERE whn = '2020-04-20'
ORDER BY confirmed DESC
```
### 7.
```sql
WITH 
    infection_rate_table AS (
    SELECT 
        c.name,
        ROUND(100000*c.confirmed/w.population,2) infection_rates
    FROM covid c JOIN world w ON c.name=w.name
    WHERE c.whn = '2020-04-20' AND w.population > 10000000
    ORDER BY w.population DESC)

SELECT *,
    RANK() OVER (ORDER BY infection_rates) rank
FROM infection_rate_table
```
### 8.
```sql
WITH
    daily_table AS (
    SELECT name, DATE_FORMAT(whn,'%Y-%m-%d') date, 
        confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) new_today
    FROM covid)

SELECT name, date, max(new_today) peak_case
FROM daily_table
WHERE new_today >= 1000
GROUP BY name, date
```
