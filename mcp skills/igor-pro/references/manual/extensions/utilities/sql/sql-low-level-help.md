---
description: "SQL XOP provides a high-level and a low-level interface to ODBC. For most users, the high-level interface, which consists of a single operation named…"
slug: /extensions/utilities/sql/sql-low-level-help
---

SQL XOP provides a high-level and a low-level interface to ODBC.

For most users, the high-level interface, which consists of a single operation named [SQLHighLevelOp](/igorpro/extensions/utilities/sql/sqlhighlevelop.md), will be sufficient. Using the high-level interface requires familiarity with SQL and basic database concepts but does not require any familiarity with ODBC.

The low-level interface consists of dozens of functions that implement most of the ODBC library functions. Using the low-level functions requires a good understanding of ODBC. It is for people who have experience programming with ODBC or are willing to spend significant time learning it.

Furthermore, the low-level interface has not been as thoroughly tested as the high-level interface and is inherently difficult to support because of its complexity and the number of functions involved.

:::caution
Do not use the low-level interface except as directed in conjunction with SQLHighLevelOp.
:::

The following low-level functions are used with [SQLHighLevelOp](/igorpro/extensions/utilities/sql/sqlhighlevelop.md):

[SQLAllocHandle](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlallochandle), [SQLFreeHandle](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlfreehandle)

[SQLConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlconnect), [SQLDriverConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldriverconnect), [SQLDisconnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldisconnect)

The use of these functions is explained under [The Multiple-Commands-Per-Connection Method](/igorpro/extensions/utilities/sql/sql-xop-high-level-programming.md#the-multiple-commands-per-connection-method).

The reasons for not using the other low-level functions are:


1. They are complicated and require a good understanding of ODBC which is quite complicated.


2. No one has used the low-level functions, other than the few listed above, since shortly after the SQL XOP was created in 2007. Consequently they have not undergone significant vetting.


3. There are too many low-level functions and too many different ways to use them and too many ODBC drivers to thoroughly test them.


4. We will not fix issues in the low-level functions other than the few mentioned in the main SQL help file.

	When we started the SQL XOP in 2007 we took the approach of exposing the ODBC API to Igor users via the low-level functions. For the reasons listed above, it became clear that supporting them would be problematic, so we created SQLHighLevelOp and strongly discouraged use of the low-level functions except for those used with SQLHighLevelOp.