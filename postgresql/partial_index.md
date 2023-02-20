# Partial Index

PostgreSQL (as well as possibly other databases) provides the functionality to create partial indices. According to the 
[docs](https://www.postgresql.org/docs/current/indexes-partial.html):  
"A partial index is an index built over a subset of a table; the subset is defined by a conditional expression (called the predicate of the partial index). The index contains entries 
only for those table rows that satisfy the predicate."


A partial index is useful when we need to query only a subset of the possible column values. For example, if we have a column specifying the status of the row and we only need to 
query for rows that are in a 'PENDING' status, a partial index will be ideal, as it reduces the total size and, by consequence, increases the perfomances.

To create a partial index:  
```
create index my_index on my_table (status) where status = 'PENDING';
```
