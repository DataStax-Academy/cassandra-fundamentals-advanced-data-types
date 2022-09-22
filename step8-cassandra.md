<!-- TOP -->
<div class="top">
  <img src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-logo.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Queries in Apache Cassandra®</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:aleksandr.volochnev@datastax.com">email</a> or <a href="https://dtsx.io/aleks">LinkedIn</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 8 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step9-cassandra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Using aggregates and functions</div>

CQL aggregates include `COUNT`, `SUM`, `AVG`, `MIN` and `MAX`. CQL also 
supports many functions, of which we will showcase `CAST`, `NOW`, and `TODATE`. 
It is also possible to create user-defined aggregates and functions using 
statements `CREATE AGGREGATE` and `CREATE FUNCTION`. We will create a function to calculate 
the number of days between two dates. Study and execute the following query examples.

✅ Q1. Analize ratings for the movie:
```
SELECT COUNT(rating) AS count,
       SUM(rating) AS sum,
       AVG(CAST(rating AS FLOAT)) AS avg,
       MIN(rating) AS min,
       MAX(rating) AS max
FROM   ratings_by_movie
WHERE  title = 'Alice in Wonderland'
  AND  year  = 2010;
```

✅ Q2. Find the user name, date of joining and current date:
```
SELECT name, 
       date_joined, 
       TODATE(NOW()) AS date_today
FROM   users
WHERE  email = 'joe@datastax.com';
```

✅ Q3. Calculate how many days passed since the user joined:
```
CREATE FUNCTION IF NOT EXISTS 
  DAYS_BETWEEN_DATES(date1 TEXT, date2 TEXT) 
RETURNS NULL ON NULL INPUT 
RETURNS BIGINT 
LANGUAGE Java AS 
'return java.lang.Math.abs(
   java.time.temporal.ChronoUnit.DAYS.between(
     java.time.LocalDate.parse(date1), 
     java.time.LocalDate.parse(date2)
   )
 );';

SELECT name, 
       DAYS_BETWEEN_DATES( 
         CAST(date_joined   AS TEXT), 
         CAST(TODATE(NOW()) AS TEXT) ) AS days
FROM   users
WHERE  email = 'joe@datastax.com';
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step9-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

