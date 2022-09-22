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
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-top-left">⬅️ Back
 </a>
<span class="step-count"> Step 1 of 11</span>
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]' 
    class="btn btn-dark navigation-top-right">Next ➡️
  </a>
</div>

<!-- CONTENT -->

<div class="step-title">Querying tables</div>

CQL queries look just like SQL queries. However, while you will see familiar clauses `SELECT`, `FROM`, `WHERE`, `GROUP BY` 
and `ORDER BY`, CQL queries are much more restrictive in what goes into those clauses. 

A CQL query can only retrieve data from a single table, so there are no joins, self-joins, nested queries, unions, intersections and so forth. 
Moreover, only columns that are declared in table's `PRIMARY KEY` definition can be used to filter, group or order rows. 
The *primary key definition order* must be respected when filtering and grouping, such that a complete partition key must be used and 
when a clustering key column is used, any preceding clustering column in the primary key definition must also be used. 
When ordering rows, the *clustering order* declared in the table definition must be respected. Ordering only applies to rows within a partition and can be either preserved or reversed.

These restrictions ensure that your queries only use efficient data access patterns, which include *retrieving one row*, 
*retrieving all rows or a subset of rows from one partition* and *retrieving rows from at most a few partitions*. 
The smaller the number of partitions a query touches, the better performance and throughput can be expected. When studying 
our query examples in this tutorial, pay attention to data access patterns they implement.

<!-- NAVIGATION -->
<div id="navigation-bottom" class="navigation-bottom">
 <a href='command:katapod.loadPage?[{"step":"intro"}]'
   class="btn btn-dark navigation-bottom-left">⬅️ Back
 </a>
 <a href='command:katapod.loadPage?[{"step":"step2-cassandra"}]'
    class="btn btn-dark navigation-bottom-right">Next ➡️
  </a>
</div>
