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
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 9 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step10-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Grouping rows</div>

Some queries may need to organize rows into groups 
and compute aggregates for each individual group. In Cassandra, 
grouping is always based on partition and clustering key columns and
must follow the primary key definition order. In other words, a group 
is always defined as a set of rows belonging to the same partition.
Consider the following query examples.

✅ Q1. Calculate average ratings for all movies:
```
SELECT   title, year,
         AVG(CAST(rating AS FLOAT)) AS avg_rating
FROM     ratings_by_movie
GROUP BY title, year;
```

✅ Q2. Calculate the number of ratings per user:
<details>
  <summary>Solution</summary>
  
```
SELECT   email, COUNT(rating) AS n
FROM     ratings_by_user
GROUP BY email;
```

</details> 

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step10-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

