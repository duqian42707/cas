---
layout: default
title: CAS - Password Management
category: Password Management
---

{% include variables.html %}

# Password Management - JDBC

The account password and security questions may be stored inside a database.

JDBC support is enabled by including the following dependencies in the WAR overlay:

{% include_cached casmodule.html group="org.apereo.cas" module="cas-server-support-pm-jdbc" %}

{% include_cached casproperties.html properties="cas.authn.pm.jdbc" %}

The expected database schema for the user accounts is:

```sql
create table pm_table_accounts (id int, userid varchar(255), password varchar(255), 
    email varchar(255), phone varchar(255), enabled tinyint);
```

The expected database schema for account security questions is:

```sql
create table pm_table_questions (id int, userid varchar(255), question varchar(255), answer varchar(255));
```

## Password History

This feature is does also enable password history tracking and storage. Managing 
passwords via JDBC will switch CAS to use the same JDBC configuration for password history.
