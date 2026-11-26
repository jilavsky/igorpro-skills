---
description: "SQL XOP provides easy access to ODBC-compatible databases through its high-level interface which consists of a single operation named SQLHighLevelOp."
slug: /extensions/utilities/sql/sql-xop-high-level-programming
---

SQL XOP provides easy access to ODBC-compatible databases through its high-level interface which consists of a single operation named [SQLHighLevelOp](/igorpro/extensions/utilities/sql/sqlhighlevelop.md). For most applications, you can use this high-level interface and do not need to learn the details of ODBC programming.

The high-level interface provides two ways to connect to the database. These are called "one-command-per-connection" and "multiple-commands-per-connection".

SQLHighLevelOp allows you to connect to a database, execute an SQL statement, fetch results, if any, and close the connection, all in one easy step. For simple applications this one-command-per-connection method is sufficient.

For more complex applications, it is also possible, though not required, to open a connection to a database in a separate step, make multiple calls to SQLHighLevelOp using that connection, and then close the connection in another step. This multiple-commands-per-connection method provides better throughput at the cost of greater complexity.

## The One-Command-Per-Connection Method {#the-one-command-per-connection-method}

Using the one-command-per-connection method, you provide a connection string that specifies the name of the ODBC driver to use, the URL of the host computer on which the SQL database server is running, a user name, a password, and other information needed to connect to the database. The connection string may specify the required information directly or may refer to a DSN (data source name) that you have previously created which indirectly specifies some or all of the information required to connect.

In this example, the connection string specifies all of the information directly. A `SELECT` statement is then executed. SQLHighLevelOp automatically loads any results from the SQL `SELECT` statement into waves and displays them in a table:

```igor
#include <SQLConstants>
Function Test()
    String connectionStr = ""
    connectionStr += "DRIVER=MySQL ODBC 8.0 ANSI Driver;"
    connectionStr += "SERVER=ensembldb.ensembl.org;"
    connectionStr += "DATABASE=information_schema;"
    connectionStr += "UID=anonymous;"
    connectionStr += "PWD=;"
    connectionStr += "CHARSET=UTF8;"
    String statement = "Select * from CHARACTER_SETS"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} /O /E=1 statement
End
```

The SQL_DRIVER_COMPLETE flag tells SQLHighLevelOp to ask the ODBC driver to display a dialog in which the user can enter any additional required information but no dialog is necessary in this case because the information provided is sufficient to open the connection. Furthermore, not all ODBC drivers implement the dialog.
In the next example, the connection string references a DSN named IgorDemo1. Normally, "DSN=IgorDemo1;" would be all that is required. 
In order to connect to a database, ODBC needs to know the name of the ODBC driver to use for the connection, the URL or IP address of the host computer running a database server, the name of a database served by that server, and the user name and password of a user with access to that database.

Here are four representative examples of connection strings:

```igor
"DSN=IgorDemo1;"
"DSN=IgorDemo1;UID=anonymous;PWD=;"
"DRIVER={MySQL ODBC 8.0 ANSI Driver};SERVER=ensembldb.ensembl.org;DATABASE=information_schema;UID=anonymous;PWD=;CHARSET=UTF8;"
"DRIVER={MySQL ODBC 8.0 ANSI Driver};UID=anonymous;PWD=;CHARSET=UTF8;"
```

With the "MySQL ODBC 8.0 ANSI Driver", all of these methods work on Windows.

The first two connection strings provide the necessary information by reference to a previously-created DSN. With most ODBC drivers, you can include the user name and password information in the DSN so that does not need to be specified in the connection string. However the "MySQL ODBC 8.0 ANSI Driver" requires that the user name and password appear directly in the connection string, so the first method fails while the second works.

The third connection string provides all necessary information directly, without reference to a DSN.

The fourth connection string does not provide the necessary information because it does not identify the host computer or the name of the database. In this case the ODBC driver manager will call the ODBC driver which may display a dialog in which the user can enter the rest of the information. Some ODBC drivers do not support this feature and will return an error if the connection string does not contain sufficient information to make the connection. 

At a bare minimum, ODBC needs to know which ODBC driver to talk to because it is the ODBC driver that displays the dialog soliciting additional information if needed.
The third and fourth methods, which use the driver name, have the advantage of not requiring the user to create a DSN but they will fail if the actual driver name does not match the supplied string. For example, if the MySQL installer changes the name of the driver to "MySQL ODBC 5.4 ANSI Driver", these examples will fail.

For additional discussion of connection strings see [SQLDriverConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldriverconnect).

## The Multiple-Commands-Per-Connection Method {#the-multiple-commands-per-connection-method}

Using the multiple-commands-per-connection method, you provide a connection reference number returned by the [SQLConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlconnect) or [SQLDriverConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldriverconnect) functions. After executing all of your statements, you explicitly disconnect by calling the [SQLDisconnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldisconnect) function. An example using the multiple-commands-per-connection method is provided below, under [High-Level Fetching Multiple Rows Into Variables Example](#high-level-fetching-multiple-rows-into-variables-example).

The following low-level functions are used with the multiple-commands-per-connection method:

[SQLAllocHandle](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlallochandle), [SQLFreeHandle](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlfreehandle)

[SQLConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlconnect), [SQLDriverConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldriverconnect), [SQLDisconnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldisconnect)

## SQL Statement Processing {#sql-statement-processing}

Using SQLHighLevelOp you can execute most SQL commands, including these common ones:

```
CREATE TABLE, ALTER TABLE, DELETE, INSERT, SELECT, UPDATE
```

SQLHighLevelOp does not examine the statement but merely passes it to ODBC for execution.

When executing a statement that contains parameter markers (represented by the '?' symbol), you need to provide parameter data via parameter waves or variables. SQLHighLevelOp binds your parameter data to the parameter markers before executing the statement. Most but not all DBMS's support parameter markers.

SQLHighLevelOp automatically fetches any results generated by the statement's execution and stores them in output waves or variables. Results are generated by SELECT statements and some other less-common SQL statements.

SQLHighLevelOp automatically prints diagnostic information in Igor's history area in the event of an error.

## High-Level Fetching Data Into Waves Example {#high-level-fetching-data-into-waves-example}

Here is an example that fetches data from the sample MySQL database at ensembldb.ensembl.org and displays the data in a table. To run this example, you need to have the MySQL driver installed on your machine and to create the DSN as explained under SQL XOP Tutorial.

```igor
#include <SQLConstants>
Function SQLHighLevelFetchTest1()
	// This connection string references the previously-created data source name IgorDemo1.
	String connectionStr = "DSN=IgorDemo1;UID=anonymous;PWD=;"

	String statement = "Select * from CHARACTER_SETS"
	SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} /O /E=1 statement
	
	// Print output variables
	Printf "V_flag=%d, V_SQLResult=%d, V_numWaves=%d, S_waveNames=\"%s\"\r", V_flag, V_SQLResult, V_numWaves, S_waveNames
	if (strlen(S_Diagnostics) > 0)
		Printf "Diagnostics: %s\r", S_Diagnostics
	endif
End
```

SQLHighLevelOp automatically creates output waves for the results from the select command. The /E=1 flag tells SQLHighLevelOp to display the output waves in an Igor table.


## High-Level Fetching One Row Into Variables Example {#high-level-fetching-one-row-into-variables-example}

In the preceding example, we fetched multiple rows of data into Igor waves. Sometimes you want to fetch just a single row. In that case it may be more convenient to fetch the data into variables using the /VARS flag. For example:

```igor
#include <SQLConstants>
Function SQLHighLevelFetchTest1()
	// This connection string references the previously-created data source name IgorDemo1.
	String connectionStr = "DSN=IgorDemo1;UID=anonymous;PWD=;"

	String characterSetName, description
	String statement = "Select CHARACTER_SET_NAME,DESCRIPTION from CHARACTER_SETS where CHARACTER_SET_NAME='latin1'"
	SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} /VARS={characterSetName, description} statement
	Printf "%s: \"%s\"\r", characterSetName, description
	
	// Print output variables
	Printf "V_flag=%d, V_SQLResult=%d\r", V_flag, V_SQLResult
	if (strlen(S_Diagnostics) > 0)
		Printf "Diagnostics: %s\r", S_Diagnostics
	endif
End
```

If you omit the /VARS flag, SQLHighLevelOp returns fetched data in Igor waves. If you provide the /VARS flag, fetched data is returned in the specified variables. In this example, we used local variables. You can also use global variables by passing the names of NVARs or SVARs to the /VARS flag. Your variables must be numeric or string depending on the data type of the columns you are fetching.

## SQLHighLevelOp Error Handling {#sqlhighlevelop-error-handling}

A fatal error is an error that prevents SQLHighLevelOp from completing what you asked it to do. When a fatal error occurs, SQLHighLevelOp, by default, returns a non-zero result code to Igor. When Igor receives this non-zero result code it stops procedure execution and displays an error message. Attempting to access a database for which you don't have sufficient privileges, attempting to access a non-existent field, and a syntax error in your SQL statement are all examples of errors that by default are fatal.

There are some cases where you can not allow SQLHighLevelOp to return a fatal error to Igor because you need to do cleanup, for example, closing a database connection that you previously opened. To guarantee that you do the required cleanup, you have to detect and gracefully handle errors instead of allowing SQLHighLevelOp to return a fatal error to Igor.

You prevent a fatal error by using the /Z=1 flag when calling SQLHighLevelOp. With /Z=1, you are telling SQLHighLevelOp not to return an error to Igor. Instead, SQLHighLevelOp puts any error code into the variable V_flag, which you check after each call, and returns 0 to Igor signifying no error. If V_flag is non-zero, you know an error has occurred and you can proceed accordingly. An example of gracefully handling errors is shown in the next section.

In addition to V_flag, SQLHighLevelOp sets another variable, V_SQLResult, which sometimes may be of use in error handling. V_SQLResult contains the ODBC result code from the last ODBC call that SQLHighLevelOp made. In most cases V_SQLResult is of little consequence.

The following example shows a case where we do need to check V_SQLResult. In that example, we read one row after another from a result set until there are no more rows to read. We detect that there are no more rows to read by comparing V_SQLResult to SQL_NO_DATA.

## High-Level Fetching Multiple Rows Into Variables Example {#high-level-fetching-multiple-rows-into-variables-example}

In the preceding example, we fetched one row of data into Igor variables using the /VARS flag. This is perfect for situations where your query will return just one row. Usually for queries that you expect to return multiple rows, you will omit /VARS and SQLHighLevelOp will return the data in waves.

There may be cases where you prefer to receive the data in variables but expect the query to return more than one row. This can be done using /VARS and the /STMT flag, although it is considerably more complex and not needed for most applications.

To do this, you must allocate the environment handle, the connection handle and the statement handle yourself and you must free them when you are finished instead of relying on SQLHighLevelOp to do it. To guarantee that you free any allocated handles, you must use a try-catch structure, as demonstrated in this example:

```igor
#include <SQLConstants>
Function FetchRowsIntoVariables()		// Fetches multiple rows from database into local variables.
    // GetConnectionString is a function that you would define to return a connection string
    String connectionStr = GetConnectionString()

    Variable environmentRefNum = -1, connectionRefNum = -1, statementRefNum = -1
    Variable needToDisconnect = 0
    Variable rc

    Variable result = 0

    try
        // Obtain an ODBC environment reference number
        rc = SQLAllocHandle(SQL_HANDLE_ENV, 0, environmentRefNum)
        if (rc != SQL_SUCCESS)
            Print "Error while creating environment refnum."
            AbortOnValue 1, 1
        endif
        
        SQLSetEnvAttrNum(environmentRefNum, SQL_ATTR_ODBC_VERSION, 3)	// Specifies ODBC version 3.
        
        // Obtain an ODBC connection reference number
        rc = SQLAllocHandle(SQL_HANDLE_DBC, environmentRefNum, connectionRefNum)
        if (rc != SQL_SUCCESS)
            Print "Error while creating connection refnum."
            AbortOnValue 1, 2
        endif
        
        // Connect to the database server
        String outConnectionStr
        Variable outConnectionStrRequiredLength
        rc = SQLDriverConnect(connectionRefNum, connectionStr, outConnectionStr, outConnectionStrRequiredLength, SQL_DRIVER_COMPLETE)
        if (rc!=SQL_SUCCESS && rc!=SQL_SUCCESS_WITH_INFO)
            Print "Error while connecting to database."
            AbortOnValue 1, 3
        endif
        needToDisconnect = 1

        // Obtain an ODBC statement reference number
        rc = SQLAllocHandle(SQL_HANDLE_STMT, connectionRefNum, statementRefNum)
        if (rc != SQL_SUCCESS)
            Print "Error while creating statement refnum."
            AbortOnValue 1, 4
        endif

        // Database values will be fetched into these local variables.
        Variable partID, price
        String description, moddt

        Variable row = 1
        do
            String statement
            if (row == 1)
                statement = "Select * from parts"	// This statement creates the result set.
            else
                statement = ""					    // Execute no statement. We will just do a fetch of the next row.
            endif 
            SQLHighLevelOp /Z=1 /CONN=(connectionRefNum) /STMT=(statementRefNum) /VARS={partID, description, price, moddt} statement

            if (V_flag==0 && V_SQLResult==SQL_NO_DATA)
                break								// No more rows to fetch.
            endif

            if (V_flag!=0 || (V_SQLResult!=SQL_SUCCESS && rc!=SQL_SUCCESS_WITH_INFO))
                Print "Error while fetching rows from table 'parts'."
                AbortOnValue 1, 5
            endif
            
            Printf "Row=%d, partID=%d, description=\"%s\", price=%.2f, moddt=%s\r", row, partID, description, price, moddt

            row += 1
        while(1)

    catch
        result = V_abortCode
        Printf "FetchRowsIntoVariables: V_flag=%d, V_SQLResult=%d, V_numColumns=%d, V_numVars=%d\r", V_flag, V_SQLResult, V_numColumns, V_numVars
        if (strlen(S_Diagnostics) > 0)
            Printf "Diagnostics: %s\r", S_Diagnostics
        endif
    endtry

    if (statementRefNum >= 0)
        // Close the statement
        SQLCloseCursor(statementRefNum)
        SQLFreeHandle(SQL_HANDLE_STMT, statementRefNum)
    endif

    if (needToDisconnect)
        SQLDisconnect(connectionRefNum)
    endif

    if (connectionRefNum >= 0)
        // Close the connection
        SQLFreeHandle(SQL_HANDLE_DBC, connectionRefNum)
    endif

    if (environmentRefNum >= 0)
        // Free the environment handle
        SQLFreeHandle(SQL_HANDLE_ENV, environmentRefNum)
    endif

    return result	// 0 if no error.
End
```

The first time though the loop we execute "Select * from parts" which produces a result set with multiple rows. Also on this first pass, we receive the first row of results via our local variables.

On subsequent passes of the loop, we do not execute any query by virtue of passing "" as the SQL statement text. SQLHighLevelOp still does a fetch, returning subsequent rows of the result set, one row per iteration of the loop.

We test V_SQLResult set each time through the loop. When it is equal to SQL_NO_DATA, we know that there are no more rows to fetch.

## High-Level Parts Table Examples {#high-level-parts-table-examples}

The remaining high-level examples interact with a 'parts' table in a database named SQLHighLevelTestDB. If you have administrator privileges for a database server you can run these examples. Here is the setup information.

This setup assumes that you have a MySQL server running on your local machine or on another machine and that you have administrator-level privileges for the MySQL server. If you are running a different database server you will need to translate these instructions.

To start the MySQL monitor, execute this command from the Unix or Windows command line:

```bash
mysql -u <your mysql user name> -p
```

Execute these commands in MySQL monitor to create the test database and to create a user with sufficient privileges:

```sql
CREATE DATABASE SQLHighLevelTestDB;
```

If the MySQL server is running on your local machine:

```sql
GRANT ALL on SQLHighLevelTestDB.* to 'SQLHighLevelUser'@'localhost' IDENTIFIED BY 'SQLHighLevelTest';
```

If the MySQL server is running on a remote machine, use your IP number in place of localhost:

```sql
GRANT ALL on SQLHighLevelTestDB.* to 'SQLHighLevelUser'@'localhost' IDENTIFIED BY 'SQLHighLevelTest';
```

Now you must create a DSN (see SQL XOP Tutorial for instructions) with the following information:

```
Data Source Name:   SQLHighLevelTestDB
Description:        Test database for SQLHighLevelOp operation
Server:             localhost (or the IP address of the remote MySQL server)
User:               SQLHighLevelTestDB
Character Set:      F8
```

## General Utility Routines {#general-utility-routines}

A WaveMetrics-provided procedure file, SQLConstants.ipf, defines symbolic constants that are used in all SQL programming. Thus you need to have this statement in your main procedure window or in some other procedure window.

```igor
#include <SQLConstants>     // Include SQL symbolic constants.
```

Another WaveMetrics-provided procedure file, SQLUtils.ipf, provides some utility routines. You will rarely need these.


## High-Level Example Utility Routines {#high-level-example-utility-routines}

These additional utility routines are used by all of the parts table examples in this help file.

```igor
Function/S GetPartsDBConnectionString()	// This connection string is used to connect to the database.
    String connectionStr = "DSN=SQLHighLevelTestDB;"
    connectionStr += "UID=SQLHighLevelUser;PWD=SQLHighLevelTest;"	// Needed by MySQL ODBC driver on Macintosh
    return connectionStr
End

Function FetchPartsTable()			// Called to display parts table after we do an insert, update or delete.
    String connectionStr = GetPartsDBConnectionString()
    String statement = "Select * from parts"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} /O /E=3 statement
End

Function StorePartsTable()			// Overwrites database table from Igor waves.
    String connectionStr = GetPartsDBConnectionString()
    String statement

    statement = "Delete from parts"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} /O /E=3 statement
    PrintSQLHighLevelDiagnostics("Delete all rows", V_flag, V_SQLResult, V_SQLRowCount, V_numWaves, S_waveNames, S_diagnostics)

    statement = "INSERT INTO parts VALUES (?,?,?,?)"
    Wave partID,  price, moddt
    Wave/T description
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /PWAV={partID, description, price, moddt} statement
    PrintSQLHighLevelDiagnostics("Insert from waves", V_flag, V_SQLResult, V_SQLRowCount, V_numWaves, S_waveNames, S_diagnostics)
End

Function PrintSQLHighLevelDiagnostics(testTitle, flag, SQLResult, rowCount, numWaves, waveNames, diagnostics)
    String testTitle
    Variable flag, SQLResult, rowCount, numWaves
    String waveNames, diagnostics

    // Print output variables
    Printf "%s: V_flag=%d, V_SQLResult=%d, V_SQLRowCount=%d, V_numWaves=%d, S_waveNames=\"%s\"\r", testTitle, flag, SQLResult, rowCount, numWaves, waveNames
    if (strlen(diagnostics) > 0)
        Printf "Diagnostics: %s\r", diagnostics
    endif
End
```

## High-Level Inserting Data From Waves Example {#high-level-inserting-data-from-waves-example}

Here is an example that creates a table in an existing database and inserts multiple rows of data into the table.

An `SQL INSERT` statement can contain literal values, like this:

```sql
INSERT INTO parts VALUES (1,'Cam shaft',250.00,now()),(2,'Valve',45.25,now())
```

or it can use parameter markers, like this:

```sql
INSERT INTO parts VALUES (?,?,?,?)
```
or it can mix literal values and parameter markers, like this:

```sql
INSERT INTO parts VALUES (1,?,?,now())
```

This example shows both methods.

`now()` is a MySQL function that returns the current timestamp. On other database systems, notably Microsoft SQL Server, the `now()` function does not exist and the `getdate()` function does the same thing.

"DROP TABLE IF EXISTS" is a MySQL extension that is not supported by other databases. Instead you must use "DROP TABLE" and ignore any error which would be returned if the database did not already exist.

```igor
Function CreatePartsTable1()        // Creates 'parts' table in existing SQLHighLevelTestDB database using the one-command-per-connection method.
    String connectionStr = GetPartsDBConnectionString()

    String statement

    // "DROP TABLE IF EXISTS" is a MySQL extension that is not supported by other databases.
    statement = "DROP TABLE IF EXISTS parts"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} statement
    if (V_flag != 0)
        Print "Error while dropping table 'parts'."
        return -1
    endif

    statement = "CREATE TABLE parts (partID int NOT NULL, description varchar(100) default NULL, price float default NULL, moddt datetime default NULL, PRIMARY KEY (partID))"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} statement
    if (V_flag != 0)
        Print "Error while creating table 'parts'."
        return -1
    endif

    // This shows two different but equivalent ways to insert values
    if (0)
        // Insert multiple rows using literal strings.
        // now() is a MySQL function. On other systems you may need to use getdate() instead.
        statement = "INSERT INTO parts VALUES (1,'Cam shaft',250.00,now()),(2,'Valve',45.25,now()),(3,'Throttle',125.30,now()),(4,'Windshield',398.00,now()),(5,'Fender',202.00,now()),(6,'Motor',1395.00,now())"
        SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} statement
    else
        // Insert multiple rows using parameter waves.
        Make/O tempPartNums = {1, 2, 3, 4, 5, 6}
        Make/O/T tempDescriptions = {"Cam shaft", "Valve", "Throttle", "Windshield", "Fender", "Motor"}
        Make/O tempPrices = {250.00, 45.25, 125.30, 398.00, 202.00, 1395.00}
        // now() is a MySQL function. On other systems you may need to use getdate() instead.
        statement = "INSERT INTO parts VALUES (?,?,?,now())"
        SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /PWAV={tempPartNums, tempDescriptions, tempPrices} statement
        KillWaves/Z tempPartNums, tempDescriptions, tempPrices
    endif
    PrintSQLHighLevelDiagnostics("Insert, one-command-per-connection method.", V_flag, V_SQLResult, V_SQLRowCount, V_numWaves, S_waveNames, S_diagnostics)
    if (V_flag != 0)
        Print "Error while inserting data into table 'parts'."
        return -1
    endif

    FetchPartsTable()

    return 0
End
```

As shown in this example, if your statement uses parameter markers, you must supply parameter waves using the /PWAV or /PLST flag (or you can use parameter variables with the /PVAR flag as explained below).

If you omit /PWAV and /PLST, SQLHighLevelOp assumes the statement contains no parameter markers and executes the INSERT statement once.

If you specify /PWAV or /PLST, by default SQLHighLevelOp executes the INSERT statement once for each row of the parameter waves. In this example, we are passing parameter waves with six rows so SQLHighLevelOp will execute the INSERT statement six times, once for each row in the parameter waves.

By default, the number of rows in the first parameter wave determines the number of times the INSERT statement is executed. You can insert a subset of wave rows using the /ROWS flag.

Normally all parameter waves should have the same number of rows. In the event that some parameter waves have fewer rows than the first parameter wave, SQLHighLevelOp sets the corresponding values in the database to NULL.

To insert a null value for an entire column you can pass NULL in the list of values. For example:

```sql
INSERT INTO parts VALUES (1,'Cam shaft',NULL,now()),(2,'Valve',NULL,now())
```

or if you use parameter markers:

```sql
INSERT INTO parts VALUES (?,?,NULL,now())
```

You can insert a default value using the same syntax but DEFAULT instead of NULL. This would be appropriate for a column that is set to be auto-incrementing.

## High-Level Inserting Data From Variables Example {#high-level-inserting-data-from-variables-example}

In the preceding example, we inserted multiple rows into the database, passing parameter data via waves. To insert a single row, it may be more convenient to pass parameter data using variables. In this example, we insert a single row into an existing table.

This technique uses the /PVAR flag which requires Igor Pro 6.10 or later. With earlier versions of Igor Pro, SQLHighLevelOp with /PVAR will return an error.

```igor
Function InsertOneRowInPartsTable(partID, description, price)
    Variable partID
    String description
    Variable price

    String connectionStr = GetPartsDBConnectionString()

    String statement

    // now() is a MySQL function. On other systems you may need to use getdate() instead.
    statement = "INSERT INTO parts VALUES (?,?,?,now())"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /PVAR={partID,description,price} statement

    PrintSQLHighLevelDiagnostics("Insert a row using variables.", V_flag, V_SQLResult, V_SQLRowCount, V_numWaves, S_waveNames, S_diagnostics)
    if (V_flag != 0)
        Print "Error while inserting data into table 'parts'."
        return -1
    endif

    FetchPartsTable()

    return 0
End
```

When you use the /PVAR flag, SQLHighLevelOp takes parameter data from the listed variables which may be local variables or global variables referenced by NVAR or SVAR references. In this case we are using function parameters which behave like local variables whose values are set by the calling function. You can not pass literal values (e.g., 123 or "Hello") as parameters to /PVAR - you must pass the names of variables.

To insert a null or default value, specify `NULL` or `DEFAULT` in the statement instead of a parameter marker and omit the corresponding variable in the /PVAR flag.

## Using Parameter Waves Versus Literal Strings {#using-parameter-waves-versus-literal-strings}

As shown under [High-Level Inserting Data From Waves Example](#high-level-inserting-data-from-waves-example), you can provide values for modifying a table directly in the statement being executed or using parameter waves. Here is a simplified example:

```igor
// Insert multiple rows using literal strings
statement = "INSERT INTO parts VALUES (1,'Cam shaft',250.00,now()),(2,'Valve',45.25,now()),(3,'Throttle',125.30,now()),(4,'Windshield',398.00,now()),(5,'Fender',202.00,now()),(6,'Motor',1395.00,now())"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} statement

// Insert multiple rows using parameter waves
Make/O tempPartNums = {1, 2, 3, 4, 5, 6}
Make/O/T tempDescriptions = {"Cam shaft", "Valve", "Throttle", "Windshield", "Fender", "Motor"}
Make/O tempPrices = {250.00, 45.25, 125.30, 398.00, 202.00, 1395.00}
statement = "INSERT INTO parts VALUES (?,?,?,now())"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /PWAV={tempPartNums, tempDescriptions, tempPrices} statement
```

We call the second technique "batch row processing" and is discussed in the next section. It is convenient when the parameters for the statement are already stored in waves since it relieves you of the need to programmatically create a large statement string.

In testing with four columns and 10000 rows using MyODBC 8.0.20 on Windows accessing a MySQL server on another machine on the local area network, we found that the literal string method is much faster, 66 times faster to be precise. This surprising result held even though the literal statement string was constructed by concatenation to a length of several megabytes.

It is possible that other ODBC drivers may behave dramatically differently. In cases where you are inserting or updating large numbers of rows, you can test the speed different experimentally or you can go straight to the literal string technique.

## Batch Row Processing Using Parameter Waves {#batch-row-processing-using-parameter-waves}

As shown under [High-Level Inserting Data From Waves Example](#high-level-inserting-data-from-waves-example), you can use the SQLHighLevelOp /PWAV flag to pass values to be used in SQL statements in waves. The waves can provide values for multiple database rows.

By default, SQLHighLevelOp executes the statement once for each row in the parameter waves. You can restrict this to a subset of the wave rows using the /ROWS={startRow, endRow} flag. Whether you are using all wave rows or a subset, by default SQLHighLevelOp executes the statement once for each row.

If you are inserting or updating a large number of rows, executing the statement once for each row can be slow. Starting with SQL XOP 1.60 (first shipped with Igor Pro 9.00), you can tell SQLHighLevelOp to use batches of wave rows at one time. You do this using the optional rowsPerBatch parameter to the /ROWS flag.

In the high-level updating example, you can do this update all rows in one batch using /ROWS={-1,-1,-1}. The first -1 means "use the default starting row, row 0". The second -1 means "use the default ending row, row n-1 for an n-point wave". The third -1 means "use n for the number of rows to process at a time". Thus, /ROWS={-1,-1,-1} means "process all wave rows in one batch".

In the example, which updates 6 rows, using /ROWS={-1,-1,3} would tell SQLHighLevelOp to use a batch size of 3. This would result in executing two batches of three rows each. Breaking the operation into multiple batches like this may be useful when you are inserting or updating a very large number of rows to reduce memory requirements and if your ODBC driver does not like to process a huge amount of data in one call.

In testing with four columns and 10000 rows using MyODBC 8.0.20 on Windows accessing a MySQL server on another machine on the local area network, we found that the time to complete the statement was about the same whether we 1 or 10000 for rowsPerBatch. Also passing values as literals in the statement string was significantly faster than using parameter waves - see [Using Parameter Waves Versus Literal Strings](#using-parameter-waves-versus-literal-strings). It is possible that other ODBC drivers may behave dramatically differently.

Unfortunately some ODBC drivers do not support batch row processing. For example, as of version 8.0.20, the MyODBC driver from MySQL does not support batch processing on Macintosh. It does support it on Windows. See [https://bugs.mysql.com/bug.php?id=95608](https://bugs.mysql.com/bug.php?id=95608) for technical details. Also, batch processing may work with some SQL statements and not with others because of bugs or driver limitations.

SQL XOP attempts to detect these problems and fall back to one-row-at-a-time, but it is not always possible to detect them. Therefore you need to test your application and verify that it works.


## High-Level Multiple-Commands-Per-Connection Method Example {#high-level-multiple-commands-per-connection-method-example}

This example does the same thing as the CreatePartsTable1 example - it creates a table in an existing database and inserts data into the table.

In the previous example, we used the one-command-per-connection method meaning that we provided a connection string to SQLHighLevelOp using the /CSTR flag. It connected, executed the statement, and disconnected from the database.

In this example we use the multiple-commands-per-connection method. We use the low-level [SQLAllocHandle](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlallochandle) and [SQLDriverConnect](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqldriverconnect) functions to connect to the database and obtain a connection reference number. We pass the connection reference number to SQLHighLevelOp using the /CONN flag. Rather than opening a new connection, SQLHighLevelOp uses the connection already created.

Whereas the preceding example opens and closes the connection once for every SQLHighLevelOp call, this example opens and closes the connection only once. This will result in faster execution, but it is considerably more complex. In most cases, the difference will be significant only if when doing a large number of SQLHighLevelOp calls. The simpler one-command-per-connection method is usually sufficient and the multiple-commands-per-connection method is not needed.

In ODBC, opening a connection requires first creating an "environment handle", then creating a "connection handle" and finally creating the connection. When a program is finished with the connection, it must free these handles. When we used the one-command-per-connection method, SQLHighLevelOp took care of these details for us. Since we are now using the multiple-command-per-connection method, we are responsible for allocating and freeing the handles, as shown below.

To guarantee that we do do the required cleanup when we are finished with the connection, we have to detect and gracefully handle errors instead of allowing Igor's normal behavior which is to abort procedure execution when an error occurs. We do this by checking the result code returned by each function call and also by using the /Z=1 flag when calling SQLHighLevelOp.

Most errors returned by SQLHighLevelOp are fatal. A fatal error is a programming error such as passing a null (uninitialized) string or an SQL error that prevents completing the task, such as trying to access a table for which you do not have sufficient privileges or trying to access a field that does not exist.

Without /Z=1, if a fatal error occurs, SQLHighLevelOp returns an error to Igor and this causes procedure execution to stop. In that case, we would have no opportunity to close the connection. With /Z=1, we are telling SQLHighLevelOp not to return an error to Igor. Instead, SQLHighLevelOp puts any error code into the variable V_flag, which we check after each call, and returns 0 to Igor signifying no error.

In this example, if a fatal error (V_flag != 0) occurs, we skip the rest of the function and just clean up what we've started by disconnecting from the database and freeing handles allocated by SQLAllocHandle. This response to errors is implemented using Igor's try-catch-endtry flow control structure.

```igor
Function CreatePartsTable2()        // Creates 'parts' table in existing SQLHighLevelTestDB database using the multiple-commands-per-connection method.
    String connectionStr = GetPartsDBConnectionString()

    Variable environmentRefNum = -1, connectionRefNum = -1
    Variable needToDisconnect = 0
    String statement
    Variable rc

    Variable result = 0

    try
        // Obtain an ODBC environment reference number
        rc = SQLAllocHandle(SQL_HANDLE_ENV, 0, environmentRefNum)
        if (rc != SQL_SUCCESS)
            Print "Error while creating environment refnum."
            AbortOnValue 1, 1
        endif
        
        SQLSetEnvAttrNum(environmentRefNum, SQL_ATTR_ODBC_VERSION, 3)   // Specifies ODBC version 3.
        
        // Obtain an ODBC connection reference number
        rc = SQLAllocHandle(SQL_HANDLE_DBC, environmentRefNum, connectionRefNum)
        if (rc != SQL_SUCCESS)
            Print "Error while creating connection refnum."
            AbortOnValue 1, 2
        endif
        
        // Connect to the database server
        String outConnectionStr
        Variable outConnectionStrRequiredLength
        rc = SQLDriverConnect(connectionRefNum, connectionStr, outConnectionStr, outConnectionStrRequiredLength, SQL_DRIVER_COMPLETE)
        if (rc!=SQL_SUCCESS && rc!=SQL_SUCCESS_WITH_INFO)
            Print "Error while connecting to database."
            AbortOnValue 1, 3
        endif
        needToDisconnect = 1

        // If the table already exists, delete it
        // "DROP TABLE IF EXISTS" is a MySQL extension that is not supported by other databases.
        statement = "DROP TABLE IF EXISTS parts"
        SQLHighLevelOp /Z=1 /CONN=(connectionRefNum) statement
        if (V_flag!=0 || (V_SQLResult!=SQL_SUCCESS && rc!=SQL_SUCCESS_WITH_INFO))
            Print "Error while dropping table 'parts'."
            AbortOnValue 1, 4
        endif

        // Create the table
        statement = "CREATE TABLE parts (partID int NOT NULL, description varchar(100) default NULL, price float default NULL, moddt datetime default NULL, PRIMARY KEY (partID))"
        SQLHighLevelOp /Z=1 /CONN=(connectionRefNum) statement
        if (V_flag!=0 || (V_SQLResult!=SQL_SUCCESS && rc!=SQL_SUCCESS_WITH_INFO))
            Print "Error while creating table 'parts'."
            AbortOnValue 1, 5
        endif
        
        // Insert data into the table
        Make/O tempPartNums = {1, 2, 3, 4, 5, 6}
        Make/O/T tempDescriptions = {"Cam shaft", "Valve", "Throttle", "Windshield", "Fender", "Motor"}
        Make/O tempPrices = {250.00, 45.25, 125.30, 398.00, 202.00, 1395.00}
        // now() is a MySQL function. On other systems you may need to use getdate() instead.
        statement = "INSERT INTO parts VALUES (?,?,?,now())"
        SQLHighLevelOp /Z=1 /CONN=(connectionRefNum) /PWAV={tempPartNums, tempDescriptions, tempPrices} statement
        KillWaves/Z tempPartNums, tempDescriptions, tempPrices
        PrintSQLHighLevelDiagnostics("Insert, multiple commands per connection method.", V_flag, V_SQLResult, V_SQLRowCount, V_numWaves, S_waveNames, S_diagnostics)
        if (V_flag!=0 || (V_SQLResult!=SQL_SUCCESS && rc!=SQL_SUCCESS_WITH_INFO))
            Print "Error while inserting data into table 'parts'."
            AbortOnValue 1, 7
        endif
    catch
        result = V_abortCode
    endtry

    if (needToDisconnect)
        SQLDisconnect(connectionRefNum)
    endif

    if (connectionRefNum >= 0)
        // Close the connection
        SQLFreeHandle(SQL_HANDLE_DBC, connectionRefNum)
    endif

    if (environmentRefNum >= 0)
        // Free the environment handle
        SQLFreeHandle(SQL_HANDLE_ENV, environmentRefNum)
    endif

    FetchPartsTable()

    return result	// 0 if no error.
End
```

## High-Level Updating Data From Waves Example {#high-level-updating-data-from-waves-example}

This example illustrates updating multiple rows of the database in one call to SQLHighLevelOp.

Here we use parameter waves. As in the INSERT example, SQLHighLevelOp executes the statement once for each row in the parameter waves.

```igor
Function UpdatePartsTable1()        // Updates 'parts' table in existing SQLHighLevelTestDB database using the one-command-per-connection method.
    String connectionStr = GetPartsDBConnectionString()

    String statement

    if (0)
        // Update multiple rows using literal strings
        // now() is a MySQL function. On other systems you may need to use getdate() instead.
        statement = "UPDATE parts SET price = 300.00, moddt=now() WHERE partID=1"   // Change Cam Shaft price.
        SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} statement
    else
        // Update multiple rows using parameter waves
        Make/O tempPartNums = {1, 2, 3, 4, 5, 6}
        Make/O tempPrices = {260.00, 55.25, 225.30, 498.00, 302.00, 2395.00}
        // now() is a MySQL function. On other systems you may need to use getdate() instead.
        statement = "UPDATE parts SET price=?, moddt=now() WHERE partID=?"
        SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /PWAV={tempPrices,tempPartNums} statement
        PrintSQLHighLevelDiagnostics("Update, one-command-per-connection method.", V_flag, V_SQLResult, V_SQLRowCount, V_numWaves, S_waveNames, S_diagnostics)
        KillWaves/Z tempPartNums, tempPrices
    endif
    if (V_flag != 0)
        Print "Error while updating data in table 'parts'."
        return -1
    endif

    FetchPartsTable()

    return 0
End
```

## High-Level Updating Data Example With Indicator Waves {#high-level-updating-data-example-with-indicator-waves}

When a value is missing the usual procedure is to set the corresponding database value to NULL. In order to do this, you need to pass length/indicator waves to SQLHighLevelOp in addition to the parameter waves.

A length/indicator wave contains either a non-negative number of characters to be stored for the corresponding parameter or a special negative indicator value, such as SQL_NULL_DATA (-1).

With SQL XOP there is usually no need to use a length/indicator wave for character parameters because, in the absence of a length/indicator wave, SQL XOP will determine the length from the text parameter wave passed into SQLHighLevelOp. Therefore length/indicator waves are needed only when you want to set a database element to NULL to distinguish an empty string (value is "") from a NULL value (value is missing). For brevity, we will refer to length/indicator waves as "indicator waves".

This example is the same as UpdatePartsTable1 except that it uses indicator waves to set one of the database elements to NULL.
ODBC ignores length values (non-negative numbers) in indicator waves for numeric columns. They are used only to indicate the length of elements of character and binary columns. That is why, in this example, we set all length/indicator values to zero except for the one corresponding to the element that we want to set to NULL.

```igor
Function UpdatePartsTable3()        // Updates 'parts' table in existing SQLHighLevelTestDB database using indicator waves.
    String connectionStr = GetPartsDBConnectionString()

    String statement
        
    Make/O/I tempPartNumIndicators = {0, 0, 0, 0, 0, 0}
    Make/O/I tempPriceIndicators = {0, SQL_NULL_DATA, 0, 0, 0, 0}           // Valve price is NULL.

    Make/O tempPartNums = {1, 2, 3, 4, 5, 6}
    Make/O tempPrices = {240.00, 35.25, 115.30, 388.00, 192.00, 1295.00}

    // now() is a MySQL function. On other systems you may need to use getdate() instead.
    statement = "UPDATE parts SET price=?, moddt=now() WHERE partID=?"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /IWAV={tempPriceIndicators, tempPartNumIndicators} /PWAV={tempPrices,tempPartNums} statement
    PrintSQLHighLevelDiagnostics("Update using indicator waves", V_flag, V_SQLResult, V_SQLRowCount, V_numWaves, S_waveNames, S_diagnostics)

    KillWaves/Z tempPartNumIndicators, tempPriceIndicators
    KillWaves/Z tempPartNums, tempPrices

    if (V_flag != 0)
        Print "Error while updating data in table 'parts'."
        return -1
    endif

    FetchPartsTable()

    return 0
End
```

## High-Level Treatment of NaN Parameter Values {#high-level-treatment-of-nan-parameter-values}

NaN means "not-a-number" and is the representation of a blank or undefined floating point value.

Some SQL servers do not handle NaN values well when used as parameters. For example, if you try to use NaN as a parameter in an INSERT or UPDATE statement, MySQL converts NaN to zero and Microsoft SQL Server returns an error. Some SQL servers may accept NaN as a legitimate value.

Since it appears that most servers have trouble with NaNs, the default behavior of SQLHighLevelOp is to treat a NaN parameter value, specified using the /PWAV or /PVAR flags, as a NULL value. This is what you need if your server does not support NaN parameters and your parameter waves or variables may contain NaN.

You can override the default to make SQLHighLevelOp pass NaN parameters as NaNs using the /OPTS=2 flag. Use this if your server accepts NaN parameters and you want to store NaN in a field.

## Date/Time Data {#date-time-data}

Date/time data includes date, time and date-and-time data.

Different database systems represent date/time data in different ways. The ODBC library and drivers convert database data as necessary to fit into one of three ODBC types: date, time, and timestamp (a combination of date and time plus fractional seconds).

In Igor, date/time data is stored in double-precision waves in Igor date/time format - namely as the number of seconds since January 1, 1904. Igor date/time waves are marked as date/time waves by setting the data units to "dat". When a date/time wave is displayed in an Igor table, the table automatically uses the date/time format. When a date/time wave is displayed in a graph, the graph displays a date/time axis. Other than that, date/time waves are just like any other double-precision numeric waves.

An Igor date/time value can also be stored in a local or global variable.

## High-Level Loading of Date/Time Data {#high-level-loading-of-date-time-data}

By default, when SQLHighLevelOp loads date, time or timestamp data from a database, as a result of a SELECT statement returning date/time values, it creates Igor date/time waves to hold the date/time data. NULL values result in NaN being stored in the corresponding wave element.

In rare cases, you may prefer to load date/time data into text waves. You can tell SQLHighLevelOp to do this by using the /OPTS=1 flag when calling SQLHighLevelOp.

You can use the /VARS flag to load data into variables rather than waves. If you load a date/time column into a numeric variable, the numeric variable will store the date/time value in Igor date/time format or NaN if the date/time value is NULL. If you load a date/time column into a string variable, the database converts the date/time value into text which is then stored in the string variable.

## High-Level Storing of Date/Time Data {#high-level-storing-of-date-time-data}

If you use a date/time wave as a parameter, for example in an `INSERT`, `DELETE` or `UPDATE` statement, SQLHighLevelOp transparently passes strings containing corresponding date/time values to ODBC for that parameter. For example, this deletes all rows whose modification date is prior to January 1, 2007:

```igor
Variable year=2007, month=01, day=01
Make/O/D/N=1 tempModDT = date2secs(year,month,day)
SetScale d 0, 0, "dat", tempModDT		// Make it a date/time wave
statement = "Delete from parts where moddt<?"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} /PWAV={tempModDT} statement
KillWaves/Z tempModDT
```

Here the parameter marker ? obtains its value from the tempModDT wave. Since the tempModDT wave is a date/time wave (double-precision with data units="dat"), SQLHighLevelOp provides ODBC with a string ("2007-01-01 00:00:00") representing the date/time value in the wave.

In this example there is no real need to use a parameter wave as it could be done with a literal value like this:

```igor
statement = "Delete from parts where moddt<\"2007-01-01\""
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} statement
```

However, if year, month and day were parameters to a function, for example, then the literal value would not work. In that case, you could use a parameter wave.

You can also use a parameter variable via the /PVAR flag for storing date/time data. Here is a modified version of the example in [High-Level Inserting Data From Variables Example](#high-level-inserting-data-from-variables-example):

```igor
Variable dt = Date2Secs(2020,06,22)	// In Igor date/time format
statement = "INSERT INTO parts VALUES (?,?,?,?)"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /PVAR={partID,description,price,dt} statement
```

However there is a problem using a variable to transmit a date/time value. As explained at [https://bugs.mysql.com/bug.php?id=77048](https://bugs.mysql.com/bug.php?id=77048), MyODBC (the MySQL ODBC driver) does not support the ODBC SQLDescribeParam function. Other ODBC drivers may have the same problem. This prevents Igor from determining that the dt value is being inserted into a date column of the database table. Consequently SQL XOP does not convert from Igor date/time format into a format acceptable to ODBC. This causes an error to occur.

Here is a workaround using a string for the date/time value:

```igor
Variable dt = Date2Secs(2020,06,22)	// In Igor date/time format
String dtStr = Secs2Date(dt, -2)		// 2020-06-22 is recognized by MyODBC
statement = "INSERT INTO parts VALUES (?,?,?,?)"
SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE_REQUIRED} /PVAR={partID,description,price,dtStr} statement
```

## Handling Binary Data With SQLHighLevelOp {#handling-binary-data-with-sqlhighlevelop}

Most database applications do not use binary data but if your application does, here is what you need to know about how SQLHighLevelOp handles it.

ODBC internally defines the binary data types `BINARY(n)`, `VARBINARY(n)`, and `LONG VARBINARY`. These store arbitrary binary data such as images or compressed data. Except for the `BINARY` type, the number of bytes of data stored can vary from row to row. The maximum length of a `BINARY` and `VARBINARY` field is different for different database systems. `BINARY` and `VARBINARY` typically support up to 65535 bytes while `LONG VARBINARY` typically supports up to 4 billion bytes.

DBMS's define various binary data types. These data types are used, for example, when defining the fields of a table.

DBMS's may or may not use the names `BINARY`, `VARBINARY` and `LONG VARBINARY`. Each DBMS has its own set of data type names. When you compose an SQL statement, you must use the DBMS-specific data type name.

For example, MySQL accepts `BINARY`, `VARBINARY` and `LONG VARBINARY`. Microsoft SQL Server accepts `BINARY` and `VARBINARY` but not `LONG VARBINARY` - you must use `IMAGE` instead.

For another example, the MySQL `LONGBLOB` data type and the Microsoft SQL Server IMAGE data type both store variable length binary data of up to 4 billion bytes. These are database-specific data type names. If you use `LONGBLOB`, it will work in MySQL but not in Microsoft SQL Server.

When SQLHighLevelOp fetches a binary column, it returns the binary data in a text wave (unless you use the /VARS flag to fetch into variables). Each row of the text wave contains all of the binary data from one row of a column of the result set. The reason for returning binary data in a text wave is that it permits SQLHighLevelOp to return a different number of bytes for each row fetched from a binary column of a database table.

:::note
Binary data can contain bytes with the value 0 anywhere. Routines internal to Igor that display strings use 0 to mean "end-of-string". Consequently, you can not reliably treat binary data as string data. For example, editing it in a table or printing it to the history may give unpredictable results. The text wave acts simply as a repository for transfering binary data from the database to Igor and from Igor back to the database.
:::

What you do with the binary data that you have read from the database depends on what the binary data represents. For example, if it represents a JPEG image, you may want to write it to a .jpg file using [FBinWrite](/igorpro/commands/fbinwrite.md) and then load it into Igor using [LoadPICT](/igorpro/commands/loadpict.md). If it represents 16-bit signed integer data, you may want to create Igor waves from it.

Depending on what you want to do with the fetched binary data, you first may have to unpack it from the text wave into numeric waves. You can call [SQLTextWaveToBinaryWaves](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqltextwavetobinarywaves) to create a series of 1D unsigned byte waves, one wave for each row in the text wave created by SQLHighLevelOp. You might then call Redimension to correct the data type and number of rows of the resulting 1D numeric waves. See [SQLTextWaveToBinaryWaves](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqltextwavetobinarywaves) for an example.

If the binary data from each row in the database contains the same number of bytes you might find it more convenient to unpack it into a single 2D wave instead of a series of 1D waves. You can call [SQLTextWaveTo2DBinaryWave](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqltextwaveto2dbinarywave) to create a single 2D unsigned byte wave, each column of which contains the binary data from one row in the text wave created by SQLHighLevelOp. You might then call Redimension to correct the data type and number of rows of the resulting 2D numeric wave. See [SQLTextWaveTo2DBinaryWave](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqltextwaveto2dbinarywave) for an example.

If you want to store binary data residing in one or more waves in the database you first need to pack it into a text wave for use in an INSERT or UPDATE statement. The [SQLBinaryWavesToTextWave](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sqlbinarywavestotextwave) and [SQL2DBinaryWaveToTextWave](/igorpro/extensions/utilities/sql/sql-xop-functions.md#sql2dbinarywavetotextwave) functions perform this packing.

## Improving Memory Management With SQLHighLevelOp {#improving-memory-management-with-sqlhighlevelop}

When SQLHighLevelOp fetches a field as a result of an `SQL SELECT` command that you have issued, it needs to allocate memory to hold the data returned from the database. It asks the ODBC driver how many bytes are needed for each field. Unfortunately, the answer returned by the driver is not always reliable for variable length text and binary fields.

For example, when fetching a potentially very large binary field, some drivers return an answer that is grossly too big. We encountered this when trying to fetch an `IMAGE` field using Microsoft SQL Server 2005 Express Edition. It returned 2,147,483,647 bytes which is the maximum number of bytes that an `IMAGE` field can hold even though the specific field we were fetching contained 2048 bytes.

This would cause SQLHighLevelOp to run out of memory for no good reason. To work around this problem, SQLHighLevelOp limits the amount of memory it will allocate for any field to 1 million bytes. After fetching the field, when the actual length of the field is known, any unneeded bytes are freed, but allocating more bytes than you need in the first place is not optimal.

If you need to load a text or binary field that exceeds 1 million bytes, you must use SQLHighLevelOp's /MFL flag, passing to it the maximum number of bytes expected for any field being fetched.

Even if you are not fetching very large fields, you can improve memory allocation by specifying the maximum number of bytes expected for any variable length field being fetched. For example, if you know that the largest field fetched using a `SELECT` statement will never have more than 2048 bytes, use /MFL=2048 to improve memory management.

## Fetching Data Into Waves With SQLHighLevelOp {#fetching-data-into-waves-with-sqlhighlevelop}

By default, SQLHighLevelOp fetches data into waves.

If you omit the /NAME flag, the wave names are determined by the names of the SQL result set that you are fetching. SQLHighLevelOp makes the waves if they do not already exist and then stores the fetched data in them.

Using the /NAME flag, you can specify the names of the waves to be created. The /NAME flag takes a semicolon-separated list of wave names. For example /NAME="wave0;wave1;wave2;" will create output waves named wave0, wave1 and wave2.

If the parameter to /NAME contains empty names, the corresponding output wave's name is determined by the corresponding column in the result set. For example /NAME="wave0;;wave2;" will create output waves named wave0 and wave2 but the name of the middle output wave will be determined by the corresponding column in the result set.

If you use the /O flag, SQLHighLevelOp overwrites existing waves with the specified name. If you omit /O, SQLHighLevelOp generates a unique name in the event of a conflict with an existing wave.

In some cases, the name generated from the column name or specified using /NAME can not be used because it conflicts with an Igor operation or function name or with a variable in the current data folder or is not a legal wave name. In these cases, SQLHighLevelOp generates a legal and unique name. You can determine the actual output wave names using the S_waveNames string variable created by SQLHighLevelOp.

The data type of the output wave is determined by SQLHighLevelOp based on the data type of the corresponding column in the result set.

If a value that you are fetching into a numeric wave is NULL, SQLHighLevelOp sets the corresponding wave point to NaN for single-precision and double-precision floating point output waves and to 0 for integer output waves.

If a value that you are fetching into a text wave is NULL, SQLHighLevelOp sets the corresponding wave point to "".

If you need to determine whether a value was NULL, you must use the /LIND flag to create length/indicator waves.

## Fetching Data Into Variables With SQLHighLevelOp {#fetching-data-into-variables-with-sqlhighlevelop}

By default, SQLHighLevelOp fetches data into waves. This is convenient when you are fetching multi-row data. For fetching a single row of data, you may prefer to use local or global variables. To do this you must use the /VARS flag. Here is an example:

```igor
#include <SQLConstants>
Function SQLHighLevelFetchTest1()
    // This connection string references the previously-created data source name IgorDemo1.
    String connectionStr = "DSN=IgorDemo1;UID=anonymous;PWD=;"

    String characterSetName, description
    String statement = "Select CHARACTER_SET_NAME,DESCRIPTION from CHARACTER_SETS where CHARACTER_SET_NAME='latin1'"
    SQLHighLevelOp /CSTR={connectionStr,SQL_DRIVER_COMPLETE} /VARS={characterSetName, description} statement
    Printf "%s: \"%s\"\r", characterSetName, description
End
```

In this example, we pass local numeric variables to /VARS. You can pass numeric or string variables as appropriate for the corresponding column in the result set.

For most types of columns, SQLHighLevelOp relies on the ODBC driver to convert from the data type of the column being fetched into double-precision floating point for numeric variables or into text for string variables. The only exception is for a date/time column being fetched into a numeric variable. In this case, SQLHighLevelOp converts the ODBC date/time value into an Igor date/time value represented as seconds since January 1, 1904.

ODBC can convert any type of column into text. For example, if you fetch a float column into an Igor string variable, the string variable will contain a textual represenation of the value of the float column.

ODBC can convert some types of columns into double-precision floating point for storage in Igor numeric variables. Any numeric column can be converted properly except that for 64-bit integer columns some loss of precision will occur. For non-numeric columns, such as text and binary, the value stored in the Igor numeric variable is undefined. Thus non-numeric columns should be fetched into string variables, not numeric variables.

If a value that you are fetching into a numeric variable is NULL, SQLHighLevelOp sets the numeric variable to NaN. There is no way for you to distinguish a non-NULL numeric value that is NaN from a NULL value using /VARS.

If a value that you are fetching into a string variable is NULL, SQLHighLevelOp sets the string variable to empty (""). There is no way for you to distinguish a non-NULL string value that is empty from a NULL string value using /VARS.

(To determine if database values are NULL you must fetch the data into waves and include the /LIND flag to create length/indicator waves.)

If the number of variables that you pass to /VARS is less than the number of columns fetched, data for extra columns is not returned by SQLHighLevelOp.

If the number of variables variables that you pass to /VARS is greater than the number of columns fetched, the extra variables are left unchanged.

See also [High-Level Fetching One Row Into Variables Example](#high-level-fetching-one-row-into-variables-example) and [High-Level Fetching Multiple Rows Into Variables Example](#high-level-fetching-multiple-rows-into-variables-example).

## Text Encodings and SQL XOP {#text-encodings-and-sql-xop}

A text encoding defines the numeric codes used to represent non-ASCII characters, such as accented characters and math symbols. This section explains how text encoding issues affect SQL XOP. It is critical only if you store non-ASCII characters in your database.

If you are running Igor7 or later, you can find background information on text encodings under [Text Encodings](/igorpro/igor-basics/text-encodings.md). This section assumes that you understand the basic concepts of text encodings.

Igor7 and later use UTF-8, a Unicode byte-oriented encoding form. The rest of this section, as well as the rest of this help file, assume that you are running Igor7 or later and thus using UTF-8.

By default in Igor, text data stored in waves or string variables is assumed to be encoded as UTF-8.

In database work, the term "character set" used instead of "text encoding".

The character set used by a database is determined when the database is created. It is possible to use a different character set for a specific table or field, but this is rarely done.

Nowadays UTF-8 is most-commonly used for databases but in olden times Latin1, a subset of the Windows western text encoding, was often used.

If you are using SQL XOP to communicate with a database that does not use UTF-8, and if you want to be able to store and retrieve non-ASCII characters, you must ensure that data transmitted from Igor to the database is converted from UTF-8 to the database's character set. Also, you must ensure that data transmitted from the database to Igor is converted to UTF-8.

With a MySQL server, you can achieve this by including the following in your connection string: CHARSET=UTF8

If you are using a DSN to provide connection information, you can include a CHARSET keyword with the value UTF8 in the DSN. This setting causes the MySQL driver to convert text from the database character set to UTF-8 or vice-versa, as needed. On Windows, in the MySQL Connector/ODBC Data Source Configuration dialog, you need to click the Details button to set the character set.

Other DBMS systems most-likely provide similar character set support.

UTF-8 can represent almost any character in any language. This is not true of other text encodings. Consequently, if your database is not using UTF-8, it is possible for you to send a character to your database that it can not represent. If you do this, the character may be converted to a question-mark or you may get an error.