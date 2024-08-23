# SQLZoo Solutions
Documenting my SQLZoo solutions.

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
8+. [Numeric Examples](#numeric-examples)
9-. [Window function](#window-function)
9+. [COVID 19](#covid-19)
9. [Self join](#self-join)
10. [Tutorial Quizzes](#tutorial-quizzews)
11. [Tutorial Student Records](#tutorial-student-records)
12. [Tutorial DDL](#tutorial-ddl)

## SELECT basics
```sql
--
SELECT population 
FROM world
WHERE name = 'Germany'
