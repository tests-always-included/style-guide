---
title: Style Guide for SQL
pageid: lang-sql


Keywords
--------

All keywords should be uppercase.

    SELECT COUNT(*)
    FROM someTable
    WHERE DATEDIFF(NOW(), someTable.timeStamp)
    ORDER BY ASC


Indentation and Whitespace
--------------------------

Clauses should be separated by newlines.

    SELECT *
    FROM someTable
    ORDER BY DESC

When SELECTing multiple columns, and place on the same line.

    SELECT this, that, and, the, other
    FROM someTable

AND should be dropped onto a newline and given an additional indentation of four spaces relative to the clause it's a part of.

    SELECT *
    FROM someTable
    WHERE column1 = true
        AND column2 = "someValue"
        AND column3 = false

IN, AS, and OR should all be placed on the same line as the clause they are a part of.

    SELECT *
    FROM someTable
    WHERE column IN config.columns

The above rules apply for all subqueries as well.

    SELECT *
    FROM (
        SELECT someTable.id AS someAlias, someTable.exampleColumn
        FROM someTable
        LIMIT 3
    )
    ORDER BY DESC

