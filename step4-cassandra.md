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
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 4 of 10</span>
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Sets</div>

A *set* is an unordered collection of distinct values. In Cassandra, sets are intended for 
storing a small number of values of the same type. To define a set data type, 
Cassandra Query Language provides construct `SET<type>`, where `type` can refer to a CQL data type like 
`INT`, `DATE`, `UUID` and so forth.

✅ As an example, alter table `movies` to add column `production` of type `SET<TEXT>`:
```
ALTER TABLE movies ADD production SET<TEXT>;
SELECT title, year, production FROM movies;
```

✅ Add three production companies for one of the movies:
```
UPDATE movies 
SET production = { 'Walt Disney Pictures', 
                   'Roth Films' }
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
UPDATE movies 
SET production = production + { 'Team Todd' } 
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
SELECT title, year, production FROM movies;
```

✅ Next, alter table `movies` to add column `genres` and 
add values *Adventure*, *Family* and *Fantasy* for one of the movies:
<details>
  <summary>Solution</summary>

```
ALTER TABLE movies ADD genres SET<TEXT>;

UPDATE movies 
SET genres = { 'Adventure', 'Family', 'Fantasy' }
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;

SELECT title, year, genres FROM movies;
```

</details>

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step5-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

