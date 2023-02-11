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
 <a href='command:katapod.loadPage?[{"step":"step4-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 5 of 10</span>
 <a href='command:katapod.loadPage?[{"step":"step6-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Lists</div>

A *list* is an ordered collection of values, where the same value may occur more than once. 
In Cassandra, lists are intended for 
storing a small number of values of the same type. To define a list data type, 
Cassandra Query Language provides construct `LIST<type>`, where `type` can refer to a CQL data type like 
`INT`, `DATE`, `UUID` and so forth.

✅ As an example, alter table `users` to add column `searches` of type `LIST<TEXT>`:
```
ALTER TABLE users ADD searches LIST<TEXT>;
SELECT id, name, searches FROM users;
```

✅ Add three latest search leterals for one of the users:
```
UPDATE users 
SET searches = [ 'Alice in Wonderland' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
UPDATE users 
SET searches = searches + [ 'Comedy movies' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
UPDATE users 
SET searches = searches + [ 'Alice in Wonderland' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT id, name, searches FROM users;
```

✅ Delete the oldest search literal and add a new one:
```
DELETE searches[0] FROM users 
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
UPDATE users 
SET searches = searches + [ 'New releases' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT id, name, searches FROM users;
```

✅ Next, alter table `users` to add column `emails` and 
add two email addresses for one of the users:
<details>
  <summary>Solution</summary> 

```
ALTER TABLE users ADD emails LIST<TEXT>;

UPDATE users 
SET emails = [ 'joe@datastax.com', 
               'joseph@datastax.com' ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

SELECT id, name, emails FROM users;
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

