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

### Solution 1
```sql
SELECT population 
FROM world
WHERE name = 'Germany'
