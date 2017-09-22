---
title: Advice for Databases
pageid: topic-db
keywords: a addresses admin adminprivilege after a_id allowed also an and append are as attribute attributes b be camelcase case conventions created database deleted deletes describes email emailaddresses emailprimary emailsecondary etc example extend for foreign from general has have how id if in individual instead it item joins key link linking modified multiple name named naming of on only override pascalcase plural preserve privilege record row rows rules should single singular soft stored such table tables the there these two use used user users when will would you
---

These rules extend and override the [general rules][general-rules].


Naming Conventions
------------------

Tables will use PascalCase and attributes of a record will use camelCase.

Linking tables will be named after the two tables it joins, such as how AdminPrivilege would link Admin and Privilege.

Database tables will be named in the singular when an individual row in the table describes a single item.  For example you will use `User` instead of `Users`.  The table `EmailAddresses` (a plural item) would only be used if a single record has multiple email addresses, such as `emailPrimary`, `emailSecondary`, etc.

The foreign key from A.id will be stored in B as B.A_id (preserve case on table name, append "_id").

Rows should have a `created` and `modified` attribute.  If soft deletes are allowed, there should also be a `deleted` attribute on the record.


{% include links.html %}
