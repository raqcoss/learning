# SQL cheatsheet

### Select a column
```sql
SELECT column, another_column, ...
FROM mytable;

SELECT * 
FROM mytable;
```
### Use conditionals
```sql
SELECT column, another_column, …
FROM mytable
WHERE condition
    AND/OR another_condition
    AND BETWEEN … AND …
    AND IN (…)
    AND …;
```
### Sort and limit query
```sql
SELECT column, another_column, …
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
### Multi-table queries with JOINs
The INNER JOIN is a process that matches rows from the first table and the second table which have the same key (as defined by the ON constraint) to create a result row with the combined columns from both tables. After the tables are joined, the other clauses are then applied.

```sql
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE condition(s)
```
### Looking for NULL values
```sql
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
```
