# sb_22-03-11_SQL_Joins_Exercise

## Assignment Details
### Part 1: Getting Started
SQL seed file provided for a vehicle owner database. From the provided seed data, create queries to:
- Join the two tables so that every column and record appears, regardless of if there is not an owner_id.
- Count the number of cars for each owner. Display the owners first_name, last_name and count of vehicles.
- Count the number of cars for each owner and display the average price for each of the cars as integers. Display the owners first_name, last_name, average price and count of vehicles.

The queries were uploaded as part of this exercise.

### Part 2: SQL Zoo
- [SQL Zoo - JOIN](https://sqlzoo.net/wiki/The_JOIN_operation) 
- [SQL Zoo - More JOIN Operations](https://sqlzoo.net/wiki/More_JOIN_operations) 

### DIFFICULTIES 
No difficulties. The JOINs were straight forward. Excel has causes some SQL skills to deteriorate since queries are used just to get the base raw data from the database and much of the processing and selections is in Excel. No difficulties, just mistakes like 'GRE' (Greece) when 'GER' (Germany) was needed, changing an AND to an OR but not reviewing the remainder of the statement.

The CASE / WHEN is nice to see. I have never used that level of functionality in SQL and it is nice to know it exists. The exercise also gave me a chance to brush up on SubQueries that are linked to the main query.

Actors with 15 leading roles: Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles. 

```sh
SELECT name, COUNT(*) AS NbrLeadRoles 
FROM   actor
JOIN   casting ON actor.id = actorid
WHERE  ord = 1
GROUP BY name
HAVING COUNT(*) > 14
ORDER BY name
;
```
Came very quickly. What? The result does not need the number of Roles? Well in Excel, just delete that column before sending the workbook!  

I forged ahead, found some info about EXISTS (plus some of the error messages where they suggested 'EXISTS' helped):
```sh
SELECT name 
FROM   actor
WHERE  EXISTS (
   SELECT actorid, COUNT(*)
   FROM   casting
   WHERE  actorid = actor.id 
     AND ord = 1
   GROUP BY actorid
   HAVING COUNT(*) > 14
)
ORDER BY name
;
```
The query helped me remember how to tie the 'outer' query into the results of the subquery. I tried IN (SELECT actorid, COUNT(*)) even though I knew it would fail.

It would have been nice to see some of the ZOO SQL solutions because just because the answers match, some approaches can be computationally expensive.

