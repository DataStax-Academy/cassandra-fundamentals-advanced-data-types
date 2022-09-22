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
 <a href='command:katapod.loadPage?[{"step":"step4-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 5 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Querying table "movies"</div>

Table `movies` stores information about movies, which are uniquely identified by their titles and release years.
This table has single-row partitions and 
the primary key defined as `PRIMARY KEY ((title, year))`. 
Let's first retrieve all rows from the table to learn how the data looks like and then focus 
on predicates that the primary key can support.

<br/>

✅ Q1. Retrieve all rows:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies;
```

</details>

<br/>

✅ Q2. Retrieve one row/partition:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies
WHERE title = 'Alice in Wonderland'
  AND year = 2010;
```

</details>

<br/>

✅ Q3. Retrieve two rows/partitions:
<details>
  <summary>Solution</summary>

```
SELECT * FROM movies
WHERE title = 'Alice in Wonderland'
  AND year IN (2010, 1951);
```

</details>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step4-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

