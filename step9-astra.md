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
 <a href='command:katapod.loadPage?[{"step":"step8-astra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 9 of 10</span>
 <a href='command:katapod.loadPage?[{"step":"step10-astra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">UDTs</div>

A *user-defined type (UDT)* is a custom data type composed of one or more named and typed fields. 
UDT fields can be of simple types, collection types or even other UDTs. 
Cassandra Query Language provides statements `CREATE TYPE`, `ALTER TYPE`, `DROP TYPE` and `DESCRIBE TYPE` 
to work with UDTs.

✅ Let's define UDT `ADDRESS` with four fields:
```
CREATE TYPE ADDRESS (
    street TEXT,
    city TEXT,
    state TEXT,
    postal_code TEXT
);
```

✅ Alter table `users` to add column `address` of type `ADDRESS`:
```
ALTER TABLE users ADD address ADDRESS;
SELECT name, address FROM users;
```

✅ Add an address for one of the users:
```
UPDATE users 
SET address = { street: '1100 Congress Ave',
                city: 'Austin',
                state: 'Texas',
                postal_code: '78701' }
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, address FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

UPDATE users 
SET address.state = 'TX'
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, 
       address.street      AS street, 
       address.city        AS city, 
       address.state       AS state,
       address.postal_code AS zip 
FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
```

✅ Next, alter table `users` to add column `previous_addresses` and 
add at least two previous addresses for one of the users:
<details>
  <summary>Solution</summary> 

```
ALTER TABLE users 
ADD previous_addresses LIST<FROZEN<ADDRESS>>;

UPDATE users 
SET previous_addresses = [
              { street: '10th and L St',
                city: 'Sacramento',
                state: 'CA',
                postal_code: '95814' } ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, previous_addresses FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

UPDATE users 
SET previous_addresses = previous_addresses + [
              { street: 'State St and Washington Ave',
                city: 'Albany',
                state: 'NY',
                postal_code: '12224' } ]
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
SELECT name, address, previous_addresses FROM users
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;
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

