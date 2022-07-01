## Why avoid Django queries (sometimes)

[https://youtu.be/PU0n81qaaGE?t=376](https://youtu.be/PU0n81qaaGE?t=376)

-   sometimes queries are sub-optimal
    -   very deep joins
    -   `__in` with large lists
    -   multiple .filter()/.exclude chains
-   sometimes better expressed in **SQL**
-   some SQL features aren’t available in the query language
    -   recursive queries
    -   tree structures
-   SQL functions and operators
    -   JSON path operators, date/time functions, ...

### Workaround

You can use .raw() to get all the niceness of SQL and it’ll return a Model!

### Why you might want to avoid using models (sometimes)

-   eg: want to return 3 arrays for a chart => no need to create a model!
    -   sql -> python object -> django object
    -   that extra conversion isn’t free
-   workaround: you could return JSON from the query as a string
-   Non-model tables
    -   eg: logging tables without primary key

### What the ORM is great at

-   Basic CRUD operations
-   interfaces that require building queries in steps
    -   adding predicates to SQL is painful
-   filter, exclude, filter, exclude
    -   although this can be inefficient (see above)
