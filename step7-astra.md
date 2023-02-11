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
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 7 of 10</span>
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Nested collections</div>

It is also possible to define collection data types that contain nested collections, such as *list of maps* or 
*set of sets of sets*. A nested collection definition has to be designated as `FROZEN`, which means that a nested collection 
is stored as a single blob value and manipulated as a whole. In other words, when an individual element 
of a frozen collection needs to be updated, the entire collection must be overwritten. As a result, nested collections 
are generally less efficient unless they hold immutable or rarely changing data. 

✅ Let's alter table `movies` again to be able to store movie casts and crews in column `crew` of type `MAP<TEXT,FROZEN<LIST<TEXT>>>`:
```
ALTER TABLE movies 
ADD crew MAP<TEXT,FROZEN<LIST<TEXT>>>;
SELECT title, year, crew FROM movies;
```

✅ Add a movie crew:
```
UPDATE movies 
SET crew = { 
  'cast': ['Johnny Depp', 'Mia Wasikowska'], 
  'directed by': ['Tim Burton']
 }
WHERE id = 5069cc15-4300-4595-ae77-381c3af5dc5e;
SELECT title, year, crew FROM movies;
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

