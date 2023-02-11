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
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]' 
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 3 of 10</span>
 <a href='command:katapod.loadPage?[{"step":"step4-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">UUIDs</div>

A *universally unique identifier (UUID)* is a 128-bit number that can be automatically generated and 
used to identify an entity or relationship in a Cassandra database. UUIDs 
provide an efficient way to assign unique identifiers and help to prevent accidental upserts or eliminate race conditions. 

Cassandra Query Language supports the following two UUID data types:
- `UUID` is a *Version 4 UUID* that is randomly generated. To generate a value of type `UUID`, you can use function `uuid()`.
- `TIMEUUID` is a *Version 1 UUID* that is generated based on a MAC address and a timestamp. 
To generate a value of type `TIMEUUID`, you can use function `now()`. When needed, the timestamp component of a `TIMEUUID` value 
can be extracted using functions `unixTimestampOf()` or `dateOf()`. 
Moreover, `TIMEUUID` values in clustering columns are automatically ordered based on their underlying timestamps and
can also be retrieved based on the timestamps using functions 
`minTimeuuid(timestamp)` and `maxTimeuuid(timestamp)`. 

✅ As an example, let's create table `users` with partition key `id` of type `UUID` and insert two rows:
```
DROP TABLE IF EXISTS users;
CREATE TABLE users (
  id UUID,
  name TEXT,
  age INT,
  PRIMARY KEY ((id))
);

INSERT INTO users (id, name, age) 
VALUES (7902a572-e7dc-4428-b056-0571af415df3, 
       'Joe', 25);
INSERT INTO users (id, name, age) 
VALUES (uuid(), 'Jen', 27);

SELECT * FROM users;
```

✅ Next, create table `movies` with partition key `id` of type `UUID` and insert the following two rows: 

| id                                   | title             | year | duration |
|--------------------------------------|-------------------|------|----------|
| 5069cc15-4300-4595-ae77-381c3af5dc5e |Alice in Wonderland| 2010 |   108    |
| uuid()                               |Alice in Wonderland| 1951 |    75    |

<br/>

<details>
  <summary>Solution</summary>

```
DROP TABLE IF EXISTS movies;
CREATE TABLE movies (
  id UUID,
  title TEXT,
  year INT,
  duration INT,
  PRIMARY KEY ((id))
);

INSERT INTO movies (id, title, year, duration) 
VALUES (5069cc15-4300-4595-ae77-381c3af5dc5e, 
       'Alice in Wonderland', 2010, 108);
INSERT INTO movies (id, title, year, duration) 
VALUES (uuid(), 'Alice in Wonderland', 1951, 75);

SELECT * FROM movies;
```

</details>

<br/>

✅ Finally, study this more advanced example, where `TIMEUUID` is used to both guarantee uniqueness and 
provide a timestamp for each row in table `comments_by_user`:
```
DROP TABLE IF EXISTS comments_by_user;
CREATE TABLE comments_by_user (
  user_id UUID,
  comment_id TIMEUUID,
  movie_id UUID,
  comment TEXT,
  PRIMARY KEY ((user_id), comment_id, movie_id)
);

INSERT INTO comments_by_user (user_id, comment_id, movie_id, comment) 
VALUES (7902a572-e7dc-4428-b056-0571af415df3, 
        63b00000-bfde-11d3-8080-808080808080, 
        5069cc15-4300-4595-ae77-381c3af5dc5e, 
        'First watched in 2000');
INSERT INTO comments_by_user (user_id, comment_id, movie_id, comment) 
VALUES (7902a572-e7dc-4428-b056-0571af415df3, 
        9ab0c000-f668-11de-8080-808080808080, 
        5069cc15-4300-4595-ae77-381c3af5dc5e, 
        'Watched again in 2010');
INSERT INTO comments_by_user (user_id, comment_id, movie_id, comment) 
VALUES (7902a572-e7dc-4428-b056-0571af415df3, 
        now(), 
        5069cc15-4300-4595-ae77-381c3af5dc5e, 
        'Watched again today');        

SELECT comment_id, dateOf(comment_id) AS date, comment
FROM comments_by_user
WHERE user_id = 7902a572-e7dc-4428-b056-0571af415df3;

SELECT comment_id, dateOf(comment_id) AS date, comment
FROM comments_by_user
WHERE user_id = 7902a572-e7dc-4428-b056-0571af415df3
  AND comment_id > maxTimeuuid('1999-01-01 00:00+0000')
  AND comment_id < minTimeuuid('2019-01-01 00:00+0000')
ORDER BY comment_id DESC;
```

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step4-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
