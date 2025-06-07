Indexes can optimize the performance of `WHERE` clauses by facilitating quicker row retrieval. Question is how? I see the Query Execution order it seems like ORDER BY executes long after WHERE.

indexes can optimize the performance of `WHERE` clauses by facilitating quicker row retrieval.

### Composite Index for Multi-Column Sorting

``` SQL
CREATE INDEX idx_name_dob 
 ON employees (last_name, date_of_birth); 

SELECT first_name, last_name, date_of_birth FROM employees ORDER BY last_name, date_of_birth;
```

## Tips and Best Practices

- **Limit the number of indexes.** Too many indexes can degrade performance on write operations such as `INSERT`, `UPDATE`, and `DELETE`.
- **Use composite indexes wisely.** They are beneficial when queries frequently involve sorting or filtering by multiple columns. The order of columns in a composite index is crucial for optimization.
- **Analyze query performance.** Utilize `EXPLAIN` to understand how indexes are being used in your queries. For example, `EXPLAIN SELECT * FROM employees WHERE department = 'Sales';` can show if the `department` index is being used.
- **Drop unused indexes.** Regularly review and drop indexes that are no longer used to maintain optimal performance.
- **Keep indexes up to date.** Ensure indexes reflect the current query patterns and database schema for efficiency.
- **Consider index maintenance overhead.** In databases with high transaction rates, maintaining indexes can incur overhead that impacts performance.