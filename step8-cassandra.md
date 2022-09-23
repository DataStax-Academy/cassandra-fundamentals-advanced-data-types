<!-- TOP -->
<div class="top">
  <img src="https://datastax-academy.github.io/katapod-shared-assets/images/ds-academy-logo.svg" />
  <div class="scenario-title-section">
    <span class="scenario-title">Using Advanced Data Types in Apache Cassandra®</span>
    <span class="scenario-subtitle">ℹ️ For technical support, please contact us via <a href="mailto:aleksandr.volochnev@datastax.com">email</a> or <a href="https://dtsx.io/aleks">LinkedIn</a>.</span>
  </div>
</div>

<!-- NAVIGATION -->
<div id="navigation-top" class="navigation-top">
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 8 of 10</span>
 <a href='command:katapod.loadPage?[{"step":"step9-cassandra"}]'
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Tuples</div>

A *tuple* is a fixed-length list, where values can be of different types. 
To define a tuple data type, 
Cassandra Query Language provides construct `TUPLE<type1,type2,..., typeN>`, 
where `type1` , `type2` , ... , `typeN` can refer to same or different CQL data types, including 
`INT`, `DATE`, `UUID` and so forth. 

✅ Here is an example of a `TUPLE` column:
```
ALTER TABLE users ADD full_name TUPLE<TEXT,TEXT,TEXT>;

UPDATE users 
SET full_name = ('Joe', 'The', 'Great')
WHERE id = 7902a572-e7dc-4428-b056-0571af415df3;

SELECT name, full_name FROM users;
```

Unlike UDTs, individual tuple components cannot be updated without updating the whole tuple. Therefore, 
you should *always prefer UDTs to tuples*.

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step7-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step9-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>

