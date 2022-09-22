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
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 7 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Querying table "ratings_by_movie"</div>

Table `ratings_by_movie` stores information about ratings organized by movies, 
such that each partition contains all ratings for one particular movie. 
This table has multi-row partitions and 
the primary key defined as `PRIMARY KEY ((title, year), email)`. 
Let's first retrieve all rows from the table to learn how the data looks like and then focus 
on predicates that the primary key can support.

<br/>

✅ Q1. Retrieve all rows:
<details>
  <summary>Solution</summary>

```
SELECT * FROM ratings_by_movie;
```

</details>

<br/>

✅ Q2. Retrieve one partition:
<details>
  <summary>Solution</summary>

```
SELECT * FROM ratings_by_movie
WHERE title = 'Alice in Wonderland'
  AND year  = 2010;
```

</details>

<br/>

✅ Q3. Retrieve two partitions:
<details>
  <summary>Solution</summary>

```
SELECT * FROM ratings_by_movie
WHERE title = 'Alice in Wonderland'
  AND year IN (2010, 1951);
```

</details>

<br/>

✅ Q4. Retrieve one row:
<details>
  <summary>Solution</summary>

```
SELECT * FROM ratings_by_movie
WHERE title = 'Alice in Wonderland'
  AND year  = 2010
  AND email = 'joe@datastax.com';
```

</details>

<br/>

✅ Q5 - Q6. Retrieve a subset of rows from a partition:
<details>
  <summary>Solution 1</summary>

```
SELECT * FROM ratings_by_movie
WHERE title = 'Alice in Wonderland'
  AND year  = 2010
  AND email IN ('jen@datastax.com', 
                'jim@datastax.com');
```

</details>
<details>
  <summary>Solution 2</summary>

```
SELECT * FROM ratings_by_movie
WHERE title = 'Alice in Wonderland'
  AND year  = 2010
  AND email < 'job@datastax.com';
```

</details>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

