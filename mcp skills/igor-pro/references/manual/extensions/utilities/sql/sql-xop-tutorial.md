---
description: "In this tutorial we will establish a connection to the MySQL database hosted at ensembldb.ensembl.org, execute a simple query and retrieve data for display in…"
slug: /extensions/utilities/sql/sql-xop-tutorial
---

In this tutorial we will establish a connection to the MySQL database hosted at ensembldb.ensembl.org, execute a simple query and retrieve data for display in Igor.

To do this you need to have the MySQL ODBC driver, called "MySQL Connector/ODBC", installed on your system. Instructions for downloading and installing the driver are provided below.

The MySQL ODBC driver does not allow you to host databases on your computer. That requires the MySQL server package. But in this tutorial we will concern ourselves only with accessing databases on other computers and thus we need only the driver.


## Activating the SQL XOP {#activating-the-sql-xop}

If you have not already done so, activate the SQL XOP as follows:

To activate SQL XOP for use with IGOR64:

1.	Open the "Igor Pro Folder/More Extensions (64-bit)/Utilities" folder.
2.	Make a shortcut for the SQL64.xop file and put  it in "Igor Pro User Files/Igor Extensions (64-bit)" (see [Igor Pro User Files](/igorpro/igor-basics/experiments-files-and-folders.md#igor-pro-user-files) for details).
3.	Restart Igor.

## Installing MySQL ODBC Driver On Windows {#installing-mysql-odbc-driver-on-windows}

To download the MySQL ODBC driver, go to

[http://dev.mysql.com/downloads/connector/odbc/](http://dev.mysql.com/downloads/connector/odbc/)

Download the "Windows Installer (x86, 64-bit) MSI Installer" and run it to install the 64-bit driver.

If you previously installed an earlier version, download and install the latest version. As of this writing the current version is 8.0.13 and that is what we are using at WaveMetrics.

We got an error on running the installer on Windows. The solution was to install the Visual C++ 2015-2017-2019 [redistributable package](IgorAction:BrowseURL__"https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads") and then run the ODBC installer again.

## Collecting Connection Parameters {#collecting-connection-parameters}

To connect to a database, you need to specify the URL of the database server, the name of the database you want to connect to, and your user ID and password for accessing the database server.

In this tutorial we use ensembldb.ensembl.org - a publically-accessible MySQL database that hosts genome information. This database requires that we connect as user 'anonymous' with no password. In real-life, you would use a real user name and password which you would get from the database administrator.

Because the real databases hosted by ensembldb.ensembl.org are too complex for demonstration purposes, in this tutorial we use the information_schema database - a database that is created during the MySQL server installation process.

## Creating a MySQL DSN on Windows {#creating-a-mysql-dsn-on-windows}

A DSN ("Data Source Name") encapsulates all of the information needed to connect to a database. We will create a DSN named "IgorDemo1" that encapsulates the information about our test database at ensembldb.ensembl.org.


1.	Open the "ODBC Data Source" administrator.

	On Windows 10 you can find the adminstrator by typing "ODBC Data Sources" in the "Type here to search" edit box in the task bar.

	If that fails, see this Microsoft [web page](IgorAction:BrowseURL__"https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/open-the-odbc-data-source-administrator").

	Select from the 64-bit MySQL ODBC drivers installed.


2.	Click the User DSN tab (or click System DNS if you want all users on your machine to be able to use this DSN).


3.	Click the Add button.


5.	Choose the "MySQL ODBC 8.0 ANSI Driver" (change this if necessary depending on your driver version) and click Finish. A new dialog, titled "MySQL Connector/ODBC Data Source Configuration", is displayed.


6.	In the Connector/ODBC dialog, enter the following values exactly as shown here:

    ```
    Data Source Name: IgorDemo1
    Description:      Ensemble Genome Database for Igor SQL Demo
    TCP/IP Server:    ensembldb.ensembl.org
    Port:             3306
    User:             anonymous
    Password:
    Database:         information_schema
    Character Set:    UTF8
    ```

	To see the Character Set setting, you need to click the Details button in the dialog.


7.	Click the Test button. You should get an alert saying that the connection was successful. Click OK to dismiss the alert. If the test fails, carefully check all of the settings. Also make sure that port 3306 is open on your computer.


8.	Click OK in the Connector/ODBC dialog to complete the DSN.


9.	Click OK to quit the ODBC Data Source Administrator program.

If you install a new version of the MySQL ODBC driver, it may leave your DSNs referencing the old version, so check the IgorDemo1 DSN after installing a new driver.


## Running the SQL Demo {#running-the-sql-demo}

In IGOR, choose `File→Example Experiments→Feature Demos→SQL Demo`.

Follow the instructions in that experiment.

If you get an error from MySQL, review [Creating a MySQL DSN on Windows](#creating-a-mysql-dsn-on-windows).


## Connecting to an Oracle Database on Windows {#connecting-to-an-oracle-database-on-windows}

This section describes how we connected to an Oracle database on a Windows system that previously had no Oracle software installed. Also, we were starting with no knowledge of Oracle. The process was rather painful. To spare you some of the pain, we are documenting what we did here. Keep in mind that we are still complete Oracle novices so you may need to enlist the help of a local expert.

:::note
If you have the full Oracle client software on your system, this does not apply to you. Consult your database administrator.
:::

If you are not already familiar with the basics of ODBC and especially with the idea of a DSN (data source name), go through the [SQL XOP Tutorial](/igorpro/extensions/utilities/sql/sql-xop-tutorial.md) which will explain these concepts.

We installed Oracle's "Instant Client Basic Lite" package and its "Instant Client ODBC" package. We then had to do some configuration and finally we created an ODBC DSN.

As of this writing, the current version of Oracle Instant Client is 11.1.0.7.

You must install the 64-bit package.

To carry out this procedure, you need the following pieces of information, which you can obtain from the database administrator for the database you are trying to access:

- The TCP/IP address or network name of the Oracle server
- The "system ID" (SID) for the database of interest on the server
- Your database server user name and password

Here are the steps we followed.


1.	Download the Oracle Windows "Instant Client Basic Lite" and "Instant Client ODBC" packages. When this guide was first written, these were available from

	http://www.oracle.com/technetwork/topics/winx64soft-089540.html, however that URL is no longer valid.


2.	Create a folder at "C:\Program Files\Oracle".


3.	Unzip the "Instant Client Basic Lite" archive into "C:\Program Files\Oracle". This creates "C:\Program Files\Oracle\instantclient_11_1".


4.	Rename "instantclient_11_1" as "instantclient".


5.	Unzip the "Instant Client ODBC" archive. This creates another folder at "C:\Program Files\Oracle\instantclient_11_1".


6.	Move the contents of the new instantclient_11_1 folder into the instantclient folder.


7.	Delete the now empty new instantclient_11_1 folder.

	The next step is a workaround for a bug in the Oracle ODBC driver installer. This workaround is necessary to get the Oracle ODBC driver installer to work properly.


8.	Open the instantclient folder, right-click and choose New->Text Document. Rename the document as "oraociei11.dll".


9.	Open a DOS command window by clicking the Windows Start menu and choosing All Programs->Accessories->Command Prompt.


10.	In the command window, execute these commands:

	```bash
	cd "C:\Program Files\Oracle\instantclient"
	odbc_install
	```

	You should get a message saying that the ODBC driver was successfully installed.

11.	Close the DOS command window.

	The next four steps create a "tnsnames.ora" file. This is a file that Oracle uses to determine how to connect to a database. "TNS" stands for "Transport Network Substrate" - Oracle's networking API.


12.	Open the "C:\Program Files\Oracle" folder. Right-click and choose New->Text Document. Change the new file's name to tnsnames.ora.


13.	Double-click the tnsnames.ora file. Windows will ask you how you want to open the file. Specify that you want to open it using Notepad.


14.	In Notepad, you now need to create a "service name" entry that tells Oracle how to connect to the database. You may need to contact the database administrator for the database you are trying to access to get the required information, but here is an example.

	In this example, the items red are values that you will or may need to replace to connect to your Oracle server:

	```sql
	MyOracle =
		(DESCRIPTION =
		(ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.1.123)(PORT = 1521))
		(CONNECT_DATA = (SID = MySID))
		)
	```

	`MyOracle` is the "service name" - a short name that references this entry in tnsnames.ora. Later, when you create an ODBC DSN, you will specify just the service name and the Oracle ODBC driver will look for the corresponding entry in tnsnames.ora to get the information it needs to connect to the database. You can use any name you want in place of `MyOracle`.

	`192.168.1.123` is the TCP/IP address of the computer hosting the database. You will need to replace the IP address with either the IP address or the name (e.g. oracle.somewhere.com) of the server hosting the Oracle database.

	`1521` is the TCP/IP port number for communicating with the Oracle server. In most cases, 1521 will be the correct port number.

	`MySID` is the Oracle "system ID". A system ID is a name which identifies a particular database on an Oracle server. If you don't know your SID, you will need to get it from the database administrator for the database you are trying to access.

	There are many other ways to create a service name in tnsnames.ora. If the approach above does not work for you, consult the database administrator.


15.	In Notepad, save the tnsnames.ora file.

	Now we must create a system environment variable, TNS_ADMIN, which tells the Oracle software where the tnsnames.ora file is located.


16.	Open the System control panel by clicking the Windows Start button, choosing Control Panels, and then double-clicking the System control panel.

	Click the Advanced tab and then the Environment Variables button.

	You should now be in a dialog that looks like this:

	<img src="MD_images/SQL64 Help/image_0.png" width="66.6%"/>

	In the screenshot above, the TNS_ADMIN environment variable is already created. The next step tells you how to create it on your system.


17.	Click the New button to summon the New System Variable dialog and fill the dialog out like this:

	<img src="MD_images/SQL64 Help/image_1.png" width="66.6%"/>

	Now click OK.

	The Oracle documentation does not say exactly when the Oracle software reads the TNS_ADMIN environment variable. Our experience was that we had to restart the computer to get Oracle to notice changes to TNS_ADMIN. Therefore, to avoid possible confusion . . .

	Restart your computer now.

	Now we are ready to create an ODBC DSN.


18.	Run the Windows Data Sources program (Control Panels folder->Administrator Tools folder->Data Sources).


19.	Click the User DSN tab to create a DSN available to the current user only or click the System DSN tab to create a DSN available to any user on your machine:

	<img src="MD_images/SQL64 Help/image_2.png" width="66.6%"/>


20.	Click the Add button. From the resulting list of ODBC drivers, choose "Oracle in instantclient".

	If you don't see "Oracle in instantclient" or something like that, then the Oracle ODBC driver was not properly installed.

	Click Finish.

	You should now see the "Oracle ODBC Driver Configuration" dialog.

	<img src="MD_images/SQL64 Help/image_3.png" width="66.6%"/>

	Note the TNS Service Name box and the triangle at the right end of it. Click the triangle to display a popup menu containing service names that the Oracle ODBC driver knows about. The service name (MyOracle in the example) that you created in the tnsnames.ora file, should appear in the popup menu. If it does not, then either the TNS_ADMIN environment variable is not right or the tnsnames.ora file is not right or you need to restart Windows to get the Oracle ODBC driver to recognize the TNS_ADMIN environment variable.


21.	Enter a data source name (e.g., MyOracle or any other name you want to represent this connection).

	Choose your service name from the TNS Service Name popup menu.

	Enter your user ID which you should have received from the database administrator.

	You can leave all of the settings in the tabs at the bottom on their default values.

	Click Test Connection.

	After a short delay, you should see this dialog:

	<img src="MD_images/SQL64 Help/image_4.png" width="66.6%"/>

	Enter your service name, user name and password and click OK.

	You should then see a dialog that says "Success". If you get an error, you will need to check the tnsnames.ora file and your user name and password for accuracy and make sure you have the required permission to access the database.

	If you did get "Success", you are now ready to connect to your Oracle database using SQL XOP.

	And it was just that easy!



Here are some web sites where we found useful information while working on this issue:

The Oracle FAQ web site, run by Oracle users:

[http://www.orafaq.com](http://www.orafaq.com)

The Oracle FAQ wiki, especially these pages:

[http://www.orafaq.com/wiki/Tnsnames.ora](http://www.orafaq.com/wiki/Tnsnames.ora)

[http://www.orafaq.com/wiki/ORA-12154](http://www.orafaq.com/wiki/ORA-12154)

The Instant Client release notes:

[https://www.oracle.com/ca-en/database/technologies/releasenote-odbc-ic.html](https://www.oracle.com/ca-en/database/technologies/releasenote-odbc-ic.html)

The Oracle documentation on service names:

[http://download.oracle.com/docs/cd/B19306_01/network.102/b14213/tnsnames.htm](http://download.oracle.com/docs/cd/B19306_01/network.102/b14213/tnsnames.htm)

The Oracle ODBC FAQ:

[https://www.oracle.com/technetwork/database/windows/odbcfaq-128251.pdf](https://www.oracle.com/technetwork/database/windows/odbcfaq-128251.pdf)

The Oracle 26 ODBC help:

[https://docs.oracle.com/en/database/oracle/oracle-database/26/index.html](https://docs.oracle.com/en/database/oracle/oracle-database/26/index.html)