- esults of the query are returned within the application's responses, you can use the `UNION` keyword to retrieve data from other tables within the database. This is commonly known as a SQL injection UNION attack.
- The `UNION` keyword enables you to execute one or more additional `SELECT` queries and append the results to the original query

`SELECT a, b FROM table1 UNION SELECT c, d FROM table2`

This SQL query returns a single result set with two columns, containing values from columns `a` and `b` in `table1` and columns `c` and `d` in `table2`.

For a `UNION` query to work, two key requirements must be met:

- The individual queries must return the same number of columns.
- The data types in each column must be compatible between the individual queries.

To carry out a SQL injection UNION attack, make sure that your attack meets these two requirements. This normally involves finding out:

- How many columns are being returned from the original query.
- Which columns returned from the original query are of a suitable data type to hold the results from the injected query.

## determining number of columns in the table

' ORDER BY 1-- ' ORDER BY 2-- ' ORDER BY 3-- etc.
used to determine the number of columns

`The ORDER BY position number 3 is out of range of the number of items in the select list.`

- The column in an `ORDER BY` clause can be specified by its index, so you don't need to know the names of any columns.
- When the specified column index exceeds the number of actual columns in the result set, the database returns an error, such as:


The second method involves submitting a series of `UNION SELECT` payloads specifying a different number of null values:

`' UNION SELECT NULL-- ' UNION SELECT NULL,NULL-- ' UNION SELECT NULL,NULL,NULL--`

If the number of nulls does not match the number of columns, the database returns an error, such as:
All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.

`As with the `ORDER BY` technique, the application might actually return the database error in its HTTP response, but may return a generic error or simply return no results. When the number of nulls matches the number of columns, the database returns an additional row in the result set, containing null values in each column. The effect on the HTTP response depends on the application's code. If you are lucky, you will see some additional content within the response, such as an extra row on an HTML table. Otherwise, the null values might trigger a different error, such as a `NullPointerException`. In the worst case, the response might look the same as a response caused by an incorrect number of nulls. This would make this method ineffective.`

## Database-specific syntax

On Oracle, every `SELECT` query must use the `FROM` keyword and specify a valid table. There is a built-in table on Oracle called `dual` which can be used for this purpose. So the injected queries on Oracle would need to look like:

`' UNION SELECT NULL FROM DUAL--`

use the double-dash comment sequence `--` to comment out the remainder of the original query following the injection point. On MySQL, the double-dash sequence must be followed by a space.
- hash character `#` can be used to identify a comment.
```
' UNION SELECT 'a',NULL,NULL,NULL-- 
' UNION SELECT NULL,'a',NULL,NULL-- 
' UNION SELECT NULL,NULL,'a',NULL-- 
' UNION SELECT NULL,NULL,NULL,'a'--
```
If the column data type is not compatible with string data, the injected query will cause a database error, such as:

`Conversion failed when converting the varchar value 'a' to data type int.`

EXAMPLE:

- The original query returns two columns, both of which can hold string data.
- The injection point is a quoted string within the `WHERE` clause.
- The database contains a table called `users` with the columns `username` and `password`.

In this example, you can retrieve the contents of the `users` table by submitting the input:

`' UNION SELECT username, password FROM users--`

In order to perform this attack, you need to know that there is a table called `users` with two columns called `username` and `password`

All modern databases provide ways to examine the database structure, and determine what tables and columns they contain.

## Retrieving multiple values within a single column

In some cases the query in the previous example may only return a single column.

You can retrieve multiple values together within this single column by concatenating the values together. You can include a separator to let you distinguish the combined values. For example, on Oracle you could submit the input:

`' UNION SELECT username || '~' || password FROM users--`

This uses the double-pipe sequence `||` which is a string concatenation operator on Oracle. The injected query concatenates together the values of the `username` and `password` fields, separated by the `~` character.

The results from the query contain all the usernames and passwords, for example:

`... administrator~s3cure wiener~peter carlos~montoya ...`

Different databases use different syntax to perform string concatenation. For more details, see the [[SQL CHEAT sheet]]