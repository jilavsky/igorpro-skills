---
description: "SQL XOP provides access to relational databases from IGOR procedures. It uses ODBC (Open Database Connectivity) libraries and drivers to provide this access."
slug: /extensions/utilities/sql/sql-xop
---

SQL XOP provides access to relational databases from IGOR procedures. It uses ODBC (Open Database Connectivity) libraries and drivers to provide this access.

This version of SQL XOP requires Igor Pro 8.00 or later and supports [long object names](/igorpro/igor-basics/using-igor.md#long-object-names).

Accessing databases requires IGOR programming. We assume that you have at least intermediate-level IGOR programming experience. If not you should read at least the first half of the Programming help file, starting from see [Programming Overview](/igorpro/programming/programming.md), or the first three chapters of the Programming volume of the Igor Pro manual which contains the same information.

You can get started with SQL XOP by reading this help file and doing the tutorial below. If you are not familiar with relational databases you will probably need to consult other material as well. See the [SQL and ODBC References](#sql-and-odbc-references) topic for pointers to other sources of information on SQL, ODBC and related technologies.

Before you can use SQL XOP, you need to install an ODBC driver for your specific database as explained in the tutorial section below.

## Activating the SQL XOP {#activating-the-sql-xop}

If you have not already done so, activate the SQL XOP as follows:

To activate SQL XOP for use with IGOR64:

1.	Open the "Igor Pro Folder/More Extensions (64-bit)/Utilities" folder.
2.	Make a shortcut for the SQL64.xop file and put  it in "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details).
3.	Restart Igor.

## SQL XOP Overview {#sql-xop-overview}

SQL (Structured Query Language) is a system for interacting with and controlling a relational database. It was developed in the 1970's by IBM. It is now the predominant standardized system for relational database management.

ODBC (Open Database Connectivity), first released by Microsoft in 1992, is a standard that defines a set of functions for the interaction between a client program and a SQL-compatible database server. Most widely-used database servers, including Microsoft SQL Server, Microsoft Access, FileMaker, Oracle, the MySQL database system, and many others, support ODBC.

An ODBC driver, obtained from the database management system (DBMS) supplier, mediates between the ODBC-compliant client program and the database server.

If you have access to an ODBC-compliant database server and have installed an ODBC driver for that database server, you can write an Igor program to query and manipulate databases on the server using the routines added to Igor by SQL XOP.

SQL XOP provides a high-level and a low-level interface to ODBC.

For most users, the high-level interface, which consists of a single operation named [SQLHighLevelOp](/igorpro/extensions/utilities/sql/sqlhighlevelop.md), will be sufficient. Using the high-level interface requires familiarity with SQL and basic database concepts but does not require any familiarity with ODBC.

The low-level interface consists of dozens of functions that implement most of the ODBC library functions. A few of the low-level functions (SQLAllocHandle, SQLFreeHandle, SQLConnect, SQLDriverConnect and SQLDisconnect) are used in conjunction with SQLHighLevelOp when doing more sophisticated applications. The vast majority of them are not used with SQLHighLevelOp.

Using the low-level functions requires a thorough understanding of ODBC. It is very complex and not as thoroughly tested as the high level interface.

:::caution
Do not use the low-level interface except as directed in conjunction with SQLHighLevelOp.
:::

The low-level interface is documented in a separate help file: [SQL Low-Level Help](/igorpro/extensions/utilities/sql/sql-low-level-help.md).

## ODBC Overview {#odbc-overview}

General support for ODBC is available for both Mac OS X and Windows in the form of an ODBC "driver manager". The driver manager is built into Windows. Client programs, like Igor's SQL XOP, communicate with the driver manager which communicates with ODBC drivers that communicate with database servers.

Each type of database server (e.g., Microsoft SQL Server or MySQL) has an associated ODBC driver. In order to connect to any database, you must have the ODBC driver for that database server type on your machine. Windows comes with a number of ODBC drivers pre-installed but not the driver for the widely-used MySQL. Mac OS X currently comes with no drivers installed. ODBC drivers can be obtained from the database supplier.

To connect to a database, you need to know the name or location on disk of the ODBC driver, the URL of the database server, the name of the database you want to access, and a username and password for authentication.

You can provide this information to the SQLHighLevelOp operation directly, like this:

```igor
String connectionStr = ""
connectionStr += "DRIVER=MySQL ODBC 8.0 ANSI Driver;"
connectionStr += "SERVER=<url>;"
connectionStr += "DATABASE=<database name>;"
connectionStr += "UID=<user name>;"
connectionStr += "PWD=<password>;"
connectionStr += "CHARSET=UTF8;"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} <statement>
```

In this case, "MySQL ODBC 8.0 ANSI Driver" is the name of the ODBC driver as registered with the ODBC driver manager.

You would replace \<url\>, \<database name\>, \<user name\> and \<password\> with actual parameters for your database, as illustrated in the tutorial below.

The use of the `CHARSET` keyword is explained under [Text Encodings and SQL XOP](/igorpro/extensions/utilities/sql/sql-xop-high-level-programming.md#text-encodings-and-sql-xop).

Alternatively, you can create a "data source". A data source is a named collection of settings like the ones shown above. The name of a data source is called a "DSN" (Data Source Name). "DSN" is often used synonymously with "data source".

On Windows, data source information is stored in the Windows registry. The Data Sources program (Control Panel -> System and Security -> Administrative Tools folder -> ODBC Data Sources) provides a user interface for creating data sources.

Assuming that you have created a DSN named IgorDemo1 that encapsulates the connection information shown above, you can use it with SQLHighLevelOp like this:

```igor
String connectionStr = "DSN=IgorDemo1;"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} <statement>
```

However there is a bug in the MySQL Mac OS X driver that requires that you provide the user name and password directly, like this:

```igor
String connectionStr = "DSN=IgorDemo1;"
connectionStr += "UID=<user name>;"
connectionStr += "PWD=<password>;"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} <statement>
```

In the following SQL XOP Tutorial we will go through the steps of installing a MySQL ODBC driver, creating a DSN, and connecting to a database at ensembldb.ensembl.org.

## SQL and ODBC References {#sql-and-odbc-references}

Wikipedia entry for SQL

[https://en.wikipedia.org/wiki/SQL](https://en.wikipedia.org/wiki/SQL)

A good, concise tutorial on SQL:

[https://www.firstsql.com/tutor.htm](https://www.firstsql.com/tutor.htm)

Wikipedia entry for ODBC

[https://en.wikipedia.org/wiki/Open_Database_Connectivity](https://en.wikipedia.org/wiki/Open_Database_Connectivity)

Microsoft ODBC Reference

[https://learn.microsoft.com/en-us/sql/odbc/reference/odbc-programmer-s-reference](https://learn.microsoft.com/en-us/sql/odbc/reference/odbc-programmer-s-reference)

MySQL Reference Manual

[http://dev.mysql.com/doc/](http://dev.mysql.com/doc/)

MySQL ODBC Developer Guide

[https://dev.mysql.com/doc/connector-odbc/en/](https://dev.mysql.com/doc/connector-odbc/en/)

"Inside ODBC", Microsoft Press, ISBN 1-55615-815-7

This book was written by Kyle Geiger, the chief architect of ODBC. It contains a lot of useful information for the serious ODBC programmer, as well as some impenetrable sections. Chapters 2 and 3 are rather abstract and are not essential for the ODBC programmer. This book is a supplement to the Microsoft documentation on ODBC, not a replacement for it.

## SQL XOP Revision Notes {#sql-xop-revision-notes}

|  |  |
| --- | --- |
| 1.00B01 | Initial release. |
| 1.00B02 | Changed the default behavior of /PWAV and /PVAR to treat a NaN value as a NULL value. This was done because neither MySQL or MS SQL Server handle NaNs well. MySQL treats NaN as zero. MS SQL Server returns an error: "not a valid instance of data type". You can override this, to treat a NaN as a NaN, by specifying /OPTS=2. |
|  | Fixed a crash that occurred if the server returned SQL_SUCCESS_ WITH_INFO instead of SQL_SUCCESS when fetching data into waves. |
|  | Fixed SQLHighLevelOp to treat SQL_SUCCESS_WITH_INFO as a success rather than a failure. |
|  | Added a workaround for Actual Technologies driver which does not support SQL_ATTR_ROWS_FETCHED_PTR. However Actual Technologies says they will add support for it in the near future. |
| 1.00B03 | Fixed problem where partial name match in names of fetched columns caused an unneeded and incorrect output wave name change. |
| 1.00B04 | The value "<NULL>", when passed for any parameter to [SQLTables](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqltables), causes SQL XOP to pass NULL to ODBC for the corresponding parameter. |
|  | Replaced the SQLGetConnectAttr low-level function with SQLGetConnectAttrStr and SQLGetConnectAttrNum functions. |
| 1.00B05 | Added workaround for MS Access and other DBMSes not supporting ODBC's SQLDescribeParam function. |
| 1.00B06 | Added workaround for bug in SQLite3ODBC driver which caused integer and floating point data returned from SQLHighLevelOp to be scrambled. |
| 1.00B07 | Added workaround for report of old Oracle client not supporting attributes that allow SQL XOP to determine the maximum number of bytes returned by a fetch. |
| 1.00 | Low-level routines SQLGetDataNum and SQLGetDataStr now handle NULL properly. |
| 1.10 | This version requires Igor Pro 6.20 or later. It is the first that supports IGOR64 on Macintosh. |
| 1.11 | Recompiled with XOP Toolkit 7.01 to support Igor Pro 8 on 64-bit Macintosh. |
| 1.12 | Workaround for Windows MySQL bug whereby the ODBC SQLGetDiagField(SQL_DIAG_CURSOR_ROW_COUNT) incorrectly returned 0. This happened only when using SQLHighLevelOp/PVAR and caused a crash. |
| 1.50 | This version supports [long object names](/igorpro/igor-basics/using-igor.md#long-object-names) and therefore requires Igor Pro 8.00 or later. |
| 1.60 | Added support for batch row processing with parameter waves. However it is probably of no use. See [Using Parameter Waves Versus Literal Strings](/igorpro/extensions/utilities/sql/sql-xop-high-level-programming.md#using-parameter-waves-versus-literal-strings) and [Batch Row Processing Using Parameter Waves](/igorpro/extensions/utilities/sql/sql-xop-high-level-programming.md#batch-row-processing-using-parameter-waves). |
|  | This version is intended for Igor Pro 9.00 or later but works with Igor Pro 8 also. |