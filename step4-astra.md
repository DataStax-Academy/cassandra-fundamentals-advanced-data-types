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
 <a href='command:katapod.loadPage?[{"step":"step3-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 4 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step5-astra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Querying table "users"</div>

Table `users` stores information about users who are uniquely identified by their email addresses.
This table has single-row partitions and 
the primary key defined as `PRIMARY KEY ((email))`. 
Let's first retrieve all rows from the table to learn how the data looks like and then focus 
on predicates that the primary key can support.

✅ Q1. Retrieve all rows:
```
SELECT * FROM users;
```

✅ Q2. Retrieve one row/partition:
```
SELECT * FROM users
WHERE email = 'joe@datastax.com';
```

✅ Q3. Retrieve two rows/partitions:
```
SELECT * FROM users
WHERE email IN ('joe@datastax.com',
                'jen@datastax.com');
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step3-astra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step5-astra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

