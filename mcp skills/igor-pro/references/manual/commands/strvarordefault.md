---
description: "The StrVarOrDefault function checks to see if the pathStr points to a string variable. If the string variable exists, StrVarOrDefault returns its value."
slug: /commands/strvarordefault
---

<div className="command-signature">

## <strong>StrVarOrDefault</strong> (<em>pathStr</em>, <em>defStrVal</em>) {#strvarordefault}

</div>

The StrVarOrDefault function checks to see if the *pathStr* points to a string variable. If the string variable exists, StrVarOrDefault returns its value. If the string variable does not exist, returns *defStrVal* instead.

### *Details* {#details}
Used to initialize input values of macros so they can remember their state without needing global variables to be defined first. Numeric variables use the corresponding numeric function, [NumVarOrDefault](/igorpro/commands/numvarordefault.md).

### *Examples* {#examples}

```igor
Macro foo(nval,sval)
	Variable nval=NumVarOrDefault("root:Packages:mypack:nvalSav",2)
	String sval=StrVarOrDefault("root:Packages:mypack:svalSav","Hi")

	DFREF dfSav= GetDataFolderDFR()
	NewDataFolder/O/S root:Packages
	NewDataFolder/O/S mypack
	Variable/G nvalSav= nval
	String/G svalSav= sval
	SetDataFolder dfSav
End
```