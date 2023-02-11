<!-- TOP -->
<div class="top">
  <img class="scenario-academy-logo" src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-2023.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Using Advanced Data Types in Apache Cassandra®</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:aleksandr.volochnev@datastax.com">email</a> or <a href="https://dtsx.io/aleks">LinkedIn</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step9-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 10 of 10</span>
 <a href='command:katapod.loadPage?[{"step":"finish-cassandra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Counters</div>

A *distributed counter* is a 64-bit signed integer, whose value can be efficiently modified by concurrent transactions 
without causing *race conditions*. 
Counters are useful for keeping track of various statistics by counting events or adding up integer values. 
To define a counter column, Cassandra Query Language provides data type `COUNTER`. There are 
a number of restrictions on how counters can be used in Cassandra:

- A counter cannot be set or reset. It can only be incremented or decremented. 
- A counter value does not exist until the first increment or decrement operation is performed. 
The first operation assumes the initial counter value of `0`.
- A table with one or more counter columns cannot have non-counter columns other than primary key columns. 
Counter columns cannot be primary key columns.

✅ As an example, let's create a new table to keep track of movie rating statistics:
```
DROP TABLE IF EXISTS movie_stats;
CREATE TABLE movie_stats (
  id UUID,
  num_ratings COUNTER,
  sum_ratings COUNTER,
  PRIMARY KEY ((id))
);
```

✅ Update the counters to account for two ratings of *7* and *9* for the same movie: 
```
UPDATE movie_stats 
SET num_ratings = num_ratings + 1,
    sum_ratings = sum_ratings + 7 
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
UPDATE movie_stats 
SET num_ratings = num_ratings + 1,
    sum_ratings = sum_ratings + 9 
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
SELECT * FROM movie_stats;
```


✅ Next, alter table `movie_stats` to add another `COUNTER` column to keep track of how many times each movie was watched and 
increment the counter value three times for one of the movies:
<details>
  <summary>Solution</summary> 

```
ALTER TABLE movie_stats ADD num_views COUNTER;

UPDATE movie_stats 
SET num_views = num_views + 1
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
UPDATE movie_stats 
SET num_views = num_views + 1
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
UPDATE movie_stats 
SET num_views = num_views + 1
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;

SELECT * FROM movie_stats;
```

</details>

<br/>

It is important to understand that, unlike updates on other data type columns, counter increments and decrements 
are *not idempotent*. An idempotent operation produces the same result when executed multiple times. It is 
safe to retry a timed-out idempotent operation. However, in case of counters, replaying an increment or decrement operation may result in overcounting or undercounting. Therefore, counters should only be used when an absolute precision is not required.

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step9-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"finish-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

