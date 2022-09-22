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
 <a href='command:katapod.loadPage?[{"step":"step9-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 10 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step11-cassandra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Ordering rows</div>

Cassandra does not sort rows when executing queries. Instead, a query either preserves the clustering order or reverses it
when retrieving rows from a table. Even when `ORDER BY` is not used, a query result still preserves the clustering order.
Also, remember that the clustering order applies to rows within the same partition and does not apply to rows that belong 
to different partitions.

For table `ratings_by_user` with `CLUSTERING ORDER BY (title ASC, year DESC)`, there are only two ordering options as shown below.

✅ Q1. Use the clustering order:
```
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com'
ORDER BY title ASC, year DESC;

-- ORDER BY can be omitted 
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com';
```

✅ Q2. Use the reverse clustering order:
```
SELECT * FROM ratings_by_user
WHERE email = 'jim@datastax.com'
ORDER BY title DESC, year ASC;
```

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step9-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step11-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

