---
description: "The NumVarOrDefault function checks to see if the pathStr points to a numeric variable. If the numeric variable exists, NumVarOrDefault returns its value."
slug: /commands/numvarordefault
---

<div className="command-signature">

## <strong>NumVarOrDefault</strong> (<em>pathStr</em>, <em>defVal</em>) {#numvarordefault}

</div>

The NumVarOrDefault function checks to see if the *pathStr* points to a numeric variable. If the numeric variable exists, NumVarOrDefault returns its value. If the numeric variable does not exist, returns *defVal* instead.

### *Details* {#details}
Used to initialize input values of macros so they can remember their state without needing global variables to be defined first. String variables use the corresponding numeric function, [StrVarOrDefault](/igorpro/commands/strvarordefault.md).

### *Examples* {#examples}

```igor
Function DemoNumVarOrDefault()
	Variable nVal = NumVarOrDefault("root:Packages:MyPackage:gNVal",2)
	String sVal = StrVarOrDefault("root:Packages:MyPackage:gSVal","Hello")

	Print nVal, sVal
	
	// Store values in package data folder for next time
	
	// Create package data folder if it does not yet exist
	NewDataFolder/O root:Packages
	NewDataFolder/O root:Packages:MyPackage
	
	DFREF dfr = root:Packages:MyPackage	// Get reference to package data folder
	
	// Create or overwrite globals in package data folder
	Variable/G dfr:gNVal = nVal
	String/G dfr:gSVal = sVal
	
	NVAR gNVal = dfr:gNVal
	gNVal += 1
	
	SVAR gSVal = dfr:gSVal
	gSVal += "!"
End
```