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
 <a href='command:katapod.loadPage?[{"step":"step5-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 6 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step7-astra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Querying table "ratings_by_user"</div>

Table `ratings_by_user` stores information about movie ratings organized by users, 
such that each partition contains all ratings left by one particular user.
This table has multi-row partitions and 
the primary key defined as `PRIMARY KEY ((email), title, year)`. 
Let's first retrieve all rows from the table to learn how the data looks like and then focus 
on predicates that the primary key can support.

✅ Q1. Retrieve all rows:
```
SELECT * FROM ratings_by_user;
```

✅ Q2. Retrieve one partition:
```
SELECT * FROM ratings_by_user
WHERE email = 'joe@datastax.com';
```

✅ Q3. Retrieve two partitions:
```
SELECT * FROM ratings_by_user
WHERE email IN ('joe@datastax.com',
                'jen@datastax.com');
```

✅ Q4. Retrieve one row:
```
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com'
  AND title = 'Alice in Wonderland'
  AND year  = 2010;
```

✅ Q5 - Q8. Retrieve a subset of rows from a partition:
```
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com'
  AND title = 'Alice in Wonderland'
  AND year IN (2010, 1951);
```
```
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com'
  AND title = 'Alice in Wonderland'
  AND year  > 1950;
```
```
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com'
  AND title = 'Alice in Wonderland';
```
```
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com'
  AND title < 'Charlie and the Chocolate Factory';
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step5-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step7-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

