---
title: Style Guide for SQL
pageid: lang-sql
---


Keywords
--------

All keywords should be uppercase.

    SELECT COUNT(*)
    FROM someTable
    WHERE DATEDIFF(NOW(), timeStamp)
    ORDER BY someField ASC


Indentation and Whitespace
--------------------------

Clauses should be separated by newlines.

    SELECT *
    FROM someTable
    ORDER BY someField DESC

When using `SELECT` on multiple columns, place the columns on the same line.

    SELECT this, that, and, the, other
    FROM someTable

`AND` should be dropped onto a newline and given an additional indentation of four spaces relative to the clause it's a part of.

    SELECT *
    FROM someTable
    WHERE column1 = true
        AND column2 = "someValue"
        AND column3 = false

`IN`, `AS`, and `OR` should all be placed on the same line as the clause they are a part of.

    SELECT *
    FROM someTable AS st
    WHERE column IN ("column1", "column2")

Queries embedded in other code should be offset from the rest of the code.

    return db->query("
        SELECT *
        FROM someTable
    ")

The above rules apply for all subqueries as well. Subqueries should also be started on a newline and indented an additional for space.

    SELECT *
    FROM (
        SELECT id AS someAlias, exampleColumn
        FROM someTable
        LIMIT 3
    )
    ORDER BY someField DESC

