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
 <a href='command:katapod.loadPage?[{"step":"step1-cassandra"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 2 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Syntax</div>

To retrieve data from a table, Cassandra Query Language provides statement `SELECT` with the following simplified syntax:

<pre class="non-executable-code">
SELECT [DISTINCT] * | 
       select_expression [AS column_name][ , ... ]
FROM   [keyspace_name.] table_name 
[WHERE partition_key_predicate
  [AND clustering_key_predicate]] 
[GROUP BY primary_key_column_name][ , ... ]
[ORDER BY clustering_key_column_name ASC|DESC][ , ... ]
[PER PARTITION LIMIT number]
[LIMIT number]
[ALLOW FILTERING]
</pre>

The `SELECT` clause specifies what to project into a final result. The projection list can include all columns using wildcard `*`, 
individual column names, aggregates, such as `COUNT` and `AVG`, and numerous functions that work with write-time timestamps,
TTLs, and values of various data types. It is even possible to create user-defined aggregates and functions using 
statements `CREATE AGGREGATE` and `CREATE FUNCTION`.

The `FROM` clause uses keyspace name and table name to identify an existing table. 
If a keyspace name is omitted, the current working keyspace is used.

The `WHERE` clause supplies partition and row filtering predicates. At the very least, 
*all* partition key column values should be provided. Predicates for *one or more* clustering key columns can 
further restrict the result, as long as the primary key definition order is respected. All predicates must be *equality* predicates (`=` and `IN`), 
except the last clustering key column predicate can be an *inequality* predicate (`>`, `<`, `>=`, `<=`).

The `GROUP BY` clause can group rows based on partition and clustering key columns, as long as the primary key definition order is respected.

The `ORDER BY` clause can retrieve rows from each partition based on the clustering order declared in a table definition or its reverse.
Even when `ORDER BY` is not used, a query result still preserves the clustering order.

The `PER PARTITION LIMIT` and `LIMIT` clauses are used to specify the maximum number of rows per partition or overall, respectively, 
that can appear in a final result.

Finally, `ALLOW FILTERING` allows Cassandra to scan data to execute queries. While this relaxes many restrictions on what predicates can be used in the `WHERE` clause, 
scanning is a very inefficient access pattern that should not be used in production. Only in rare cases, when a partition key is known, 
scanning rows within one partition may be ok. Even then, a new table, materialized view or secondary index should be considered instead as a better alternative. 
As a rule of thumb, you should avoid using `ALLOW FILTERING` in your queries and you can expect us to do the same in our examples.

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"step1-cassandra"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step3-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
