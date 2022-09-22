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
 <a href='command:katapod.loadPage?[{"step":"step10-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 11 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"finish-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Setting limits</div>

Finally, a query can limit the number of rows that can be returned.
This is doable with clauses `PER PARTITION LIMIT` and `LIMIT`, which can be used by themselves 
or together in the same query. 

✅ Q1. Use no limits:
```
SELECT * FROM ratings_by_user
WHERE email IN ('joe@datastax.com',
                'jim@datastax.com');
```

✅ Q2. Use the per partition limit:
```
SELECT * FROM ratings_by_user
WHERE email IN ('joe@datastax.com',
                'jim@datastax.com')
PER PARTITION LIMIT 2;
```

✅ Q3. Use the overall limit:
```
SELECT * FROM ratings_by_user
WHERE email IN ('joe@datastax.com',
                'jim@datastax.com')
LIMIT 3;
```

✅ Q4. Use both limits:
```
SELECT * FROM ratings_by_user
WHERE email IN ('joe@datastax.com',
                'jim@datastax.com')
PER PARTITION LIMIT 2
LIMIT 3;
```

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step10-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"finish-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

