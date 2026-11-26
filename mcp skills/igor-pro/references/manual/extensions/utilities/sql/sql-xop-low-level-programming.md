---
description: "SQL XOP implements about 80 functions to provide low-level access to ODBC. Use of the low-level functions requires some knowledge of ODBC."
slug: /extensions/utilities/sql/sql-xop-low-level-programming
---

SQL XOP implements about 80 functions to provide low-level access to ODBC. Use of the low-level functions requires some knowledge of ODBC. Typically this requires reading at least some of Microsoft's ODBC documentation which can be found at:

[http://msdn2.microsoft.com/en-us/library/ms714177.aspx](http://msdn2.microsoft.com/en-us/library/ms714177.aspx)

:::note
Most people do not need to use low-level programming and can use the much easier [SQL XOP High-Level Programming](/igorpro/extensions/utilities/sql/sql-xop-high-level-programming.md) instead.
:::

## SQL XOP's Implementation of ODBC {#sql-xop-s-implementation-of-odbc}

The low-level functions documented below provide an almost complete implementation of ODBC 3.0 functionality. For the most part, the XOP functions were designed to use the same parameters as standard ODBC functions. In some cases slight deviations were necessary. This file documents each of the SQL XOP functions but for more complete documentation, refer to ODBC documentation (see [SQL and ODBC References](/igorpro/extensions/utilities/sql/sql-xop.md#sql-and-odbc-references) below) on the web.

The main differences between the XOP's implementation and standard ODBC are:

**ODBC Handles**: ODBC handles are stored in the XOP and you are provided an opaque reference number for each handle. SQL XOP reference numbers are functionally equivalent to ODBC handles.

**Unsupported Data Types**: Some ODBC data types have no direct equivalents in IGOR so SQL XOP converts them to Igor variables, strings or waves.

**Distinct Functions For Numeric and String Data Types**: Some ODBC functions that can be used with either numeric or string data types have been implemented in SQL XOP as two distinct functions, one with a "Num" suffix and one with a "Str" suffix (e.g., [SQLGetDataNum](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlgetdatanum) and [SQLGetDataStr](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlgetdatastr)). You must be careful to use the correct version of the function; trying to read a string into a numeric variable or trying to read a numeric variable into a string could lead to a crash.

**Unicode**: The Unicode versions of the ODBC functions are not supported by SQL XOP.

## Pass-By-Reference Parameters {#pass-by-reference-parameters}

All SQL XOP functions return an ODBC result code as the direct function result. Therefore, any other outputs from an SQL XOP function must be returned via pass-by-reference parameters. With a pass-by-reference parameter, the SQL XOP function can change the value of the parameter and therefore return an output to you.

For example:

```igor
Variable rc                     // ODBC result code
Variable environmentRefNum      // Receives output from SQLAllocHandle
rc = SQLAllocHandle(SQL_HANDLE_ENV,0,environmentRefNum)
```

Here rc is the direct function result. environmentRefNum is a pass-by-reference output parameter. SQLAllocHandle stores a value in environmentRefNum to return a reference number to the calling user-defined function.

Only local variables in user-defined functions can be used as pass-by-reference parameters. Therefore you can not call an SQL XOP function that has a pass-by-reference parameter from Igor's command line. Thus all SQL XOP low-level programming must be done from user-defined functions.

## SQL Constants {#sql-constants}

For convenience, a large number of ODBC constants are defined in a procedure file, SQLConstants.ipf. In some cases the standard names of constants are too long for IGOR and they had to be abbreviated. You can still search for the original full name which appears in a comment to the right of the constant definition. To use the constants shown in the documentation, add this to your procedure file:

```igor
#include <SQLConstants>
```

## SQL Utility Procedures {#sql-utility-procedures}

WaveMetrics provides a file containing utility procedures that will be of use to most SQL programmers. To use the utility procedures, add this to your procedure file:

```igor
#include <SQLUtils>
```

SQLUtils.ipf #includes another file, SQLConstants.ipf, which contains symbolic constants that will be needed for all SQL programming.

## SQL XOP Function Results and Errors {#sql-xop-function-results-and-errors}

When you call an SQL XOP function, two kinds of errors that may occur: a programming error or an SQL error.

In the event of a programming error, such as passing a parameter that is out-of-bounds or passing a null (uninitialized) string, SQL XOP returns an error to Igor. Returning an error to Igor normally causes Igor to stop procedure execution and display an error dialog. If you want to handle the error yourself, call [GetRTError](/igorpro/commands/getrterror.md) immediately after the SQL XOP function to clear any runtime error.

An SQL error is an error in interacting with the database such as trying to access a table for which you do not have sufficient privileges or trying to access a field that does not exist. When an SQL error occurs, SQL XOP returns a standard SQL result code as the direct function result to the calling user-defined function but does not return an error to Igor. 

This allows the user-defined function to attempt to handle the error gracefully. You can get information about the SQL error by calling [SQLGetDiagRec](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlgetdiagrec).

Some of the SQL result codes are warnings or indicators rather than errors. For example, `SQL_SUCCESS_WITH_INFO` usually means that there is more data for you to fetch and `SQL_STILL_EXECUTING` means that an asynchronous SQL statement is not finished. To keep your Igor code simple, you can treat these as errors. If you are attempting to write a fully robust or asynchronous program, you must detect these codes and attempt to handle them gracefully. See the ODBC documentation for further information.

## Executing a Statement {#executing-a-statement}

You execute a statement by calling [SQLExecDirect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlexecdirect) or [SQLPrepare](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlprepare) followed by [SQLExecute](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlexecute). The latter technique is recommended when you need to execute the same SQL statement over and over again.

SQL statements that contain `SELECT` commands as well as some other ODBC functions generate result sets which must be read in a separate step, after the statement has been executed. A statement that generates a result is called a "query".

## Reading a Result Set {#reading-a-result-set}

To fetch data from a result set, you can write a specific routine that knows exactly what the shape and nature of the result data is or you can write a generic routine that determines the shape and nature of the data at runtime and therefore can handle any result data. For most applications you will write a specific routine. Both of these techniques are illustrated by the SQL Low-Level Demo experiment.

## Reading a Result Set In a Generic Fashion {#reading-a-result-set-in-a-generic-fashion}

To write a generic routine, you need the generating statement reference number which you obtain from [SQLAllocHandle](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlallochandle). You start by finding how many rows and columns are in the result set using [SQLNumResultRowsIfKnown](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlnumresultrowsifknown) and [SQLNumResultCols](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlnumresultcols) respectively. For each column you use [SQLDescribeCol](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldescribecol) to find the associated data type and create a uniquely named wave to hold it. Finally you use two nested loops to iterate over each row and column calling [SQLGetDataNum](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlgetdatanum) or [SQLGetDataStr](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlgetdatastr) until all results have been read.

The ParseSQLResults function in SQLUtils.ipf is an example of a generic routine. You can use ParseSQLResults or you may want to create your own customized version of it.

In most applications, you will know precisely the nature of the table you are querying and so you can write a specific routine which executes faster than a generic routine.

## Using Binding To Fetch One Row At One Time {#using-binding-to-fetch-one-row-at-one-time}

To write a specific routine that fetches results from a database of a known and fixed structure, you start by creating an Igor wave for each column in the result set. Each wave will be a numeric or text wave as appropriate for the column. The waves must be large enough to hold all of the data you expect to read to prevent truncation. You bind each wave to a column of the result set using [SQLBindCol](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlbindcol). When you call SQLFetch, the data is stored in your waves.

When binding waves to a result set, SQL XOP marks the waves as in-use so that they cannot be killed until you unbind the column or free the statement.

Advanced programmers can use SQLFetchScroll instead of SQLFetch but most applications will not need this. In most of this documentation we reference [SQLFetch](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlfetch) but [SQLFetchScroll](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlfetchscroll) can also be used.

Here is the outline of a routine that opens a connection to a database, executes a query, and fetches results:

```igor
SQLAllocHandle(SQL_HANDLE_ENV)      // Allocate environment handle
SQLSetEnvAttrNum(ODBC version = 3)
SQLAllocHandle(SQL_HANDLE_DBC)      // Allocate connection handle
SQLConnect
FetchDataFromRemoteDatabase         // This is a user-defined routine
    SQLAllocHandle(SQL_HANDLE_STMT) // Allocate statement handle
    SQLExecDirect
    FetchData                       // This is a user-defined routine
        SQLBindCol
        SQLBindCol
        SQLBindCol
        while(no more results available)
            SQLFetch                // Store result data in bound waves
        endfor
        SQLCloseCursor
    SQLFreeHandle(SQL_HANDLE_STMT)
SQLDisconnect
SQLFreeHandle(SQL_HANDLE_DBC)
SQLFreeHandle(SQL_HANDLE_ENV)
```

Using this technique, you are reading one row of the result set at a time into the bound waves. Since the result data always goes into the first point of the bound wave, the bound waves can not be the actual output waves. You must then transfer the data from the bound waves into your actual output waves. The next technique avoids the need for temporary waves by using a block cursor to load all of the result rows at once.

## Using A Block Cursor To Fetch Multiple Rows At One Time {#using-a-block-cursor-to-fetch-multiple-rows-at-one-time}

By default, [SQLFetch](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlfetch) retrieves a single row from the result set and stores it in waves that you have bound using [SQLBindCol](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlbindcol). Using the default behavior, in order to fetch all rows, you need to call SQLFetch and in a loop, once for each row in the result set.

Using a block cursor, you can fetch multiple rows with one call to SQLFetch. To set up a block cursor, you must set two attributes of the statement, like this:

SQLSetStmtAttrNum(statementRefNum, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN);

SQLSetStmtAttrNum(statementRefNum, SQL_ATTR_ROW_ARRAY_SIZE, maxExpectedRows);

The first attribute tells ODBC that you want to transfer an array of values for each column instead of the default one value for each column. This is called "column-wise" binding. SQL XOP does not support the other type of array binding called "row-wise" binding.

The second attribute tells ODBC the maximum number of values in each array as represented here by the variable maxExpectedRows. The waves that you bind to the columns must have at least that many points to avoid data truncation.

You must set the SQL_ROW_ARRAY_SIZE attribute before you bind any columns. This is not required by ODBC but is required by SQL XOP so that it can allocate the right size internal buffer when you bind a column.

You must choose a value for maxExpectedRows that is at least as large as the maximum number of rows in the result set. Ideally you would like to set it to the exact number of rows in the result set and make your output waves with exactly that number of points. With many ODBC drivers, you can get the number of rows in the result set by calling [SQLNumResultRowsIfKnown](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlnumresultrowsifknown). If SQLNumResultRowsIfKnown returns a negative number then the driver does not know how many result rows there are and you must pick an arbitrary number that is guaranteed to be large enough. If you pick a number that is too small, some of the result rows will be lost.

The block cursor technique is illustrated by the SQL Low-Level Demo experiment.

Here is the outline of a routine that opens a connection to a database, executes a query, and fetches results using a block cursor:

```igor
SQLAllocHandle(SQL_HANDLE_ENV)          // Allocate environment handle
SQLSetEnvAttrNum(ODBC version = 3)
SQLAllocHandle(SQL_HANDLE_DBC)          // Allocate connection handle
SQLConnect
FetchDataFromRemoteDatabase             // This is a user-defined routine
    SQLAllocHandle(SQL_HANDLE_STMT)     // Allocate statement handle
    SQLExecDirect
    FetchDataBlock                      // This is a user-defined routine
        Variable maxExpectedRows
        SQLNumResultRowsIfKnown(stmt, maxExpectedRows)
        if (maxExpectedRows < 0)
            maxExpectedRows = 100
        endif
        Make/O/N=(maxExpectedRows) <output waves>
        SQLSetStmtAttrNum(SQL_BIND_BY_COLUMN);
        SQLSetStmtAttrNum(SQL_ATTR_ROW_ARRAY_SIZE, maxExpectedRows);
            SQLBindCol
            SQLBindCol
            SQLBindCol
            SQLFetch                    // Store result data in bound waves
            Variable numRowsFetched     // Number of rows actually fetched
            SQLNumRowsFetched(statementRefNum, numRowsFetched)
            if (numRowsFetched < maxExpectedRows)
                Redimension/N=(numRowsFetched) <output waves>
            endif
            SQLCloseCursor
    SQLFreeHandle(SQL_HANDLE_STMT)
SQLDisconnect
SQLFreeHandle(SQL_HANDLE_DBC)
SQLFreeHandle(SQL_HANDLE_ENV)
```

The functions [SQLNumResultRowsIfKnown](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlnumresultrowsifknown) and [SQLNumRowsFetched](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlnumrowsfetched) are WaveMetrics extensions designed to make using block cursors easier and do not correspond to any single ODBC function.