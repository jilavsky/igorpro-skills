---
description: "These keywords are used in user functions to refer to global variables, to waves or to functions."
slug: /programming/keywords/object-reference-keywords
---

These keywords are used in user functions to refer to global variables, to waves or to functions.

<div className="command-signature">

## <strong>DFREF</strong> {#dfref}

</div>

DFREF is used to define a local data folder reference variable or input parameter in a user-defined function.

The syntax of the DFREF is:


```igor
DFREF localName [= path or dfr ][, localName1 [= path or dfr ]]...
```

where *dfr* stands for "data folder reference". The optional assignment part is used only in the body of a function, not in a parameter declaration.

Unlike the WAVE reference, a DFREF in the body without the assignment part does not do any lookup. It simply creates a variable whose value is null.

### *Examples* {#examples}

```igor
Function Test(dfr)
	DFREF dfr

	Variable dfrStatus = DataFolderRefStatus(dfr)

	if (dfrStatus == 0)
		Print "Invalid data folder reference"
		return -1
	endif

	if (dfrStatus & 2)          // Bit 1 set means free data folder
		Print "Data folder reference refers to a free data folder"
	endif

	if (dfrStatus == 1)
		Print "Data folder reference refers a global data folder"
		DFREF dfSav = GetDataFolderDFR()
		Print GetDataFolder(1)  // Print data folder path
		SetDataFolder dfSav
	endif

	Make/O dfr:jack=sin(x/8)    // Make a wave in the referenced data folder

	return 0
End
```

### *See Also* {#see-also}
For information on programming with data folder references, see [Data Folder References](/igorpro/programming/programming.md#data-folder-references).

<div className="command-signature">

## <strong>FUNCREF</strong> {#funcref}

</div>

Within a user function, FUNCREF is a declaration that creates a local reference to a function or a variable containing a function reference.

When passing a function as an input parameter to a user function, the syntax is:


```igor
FUNCREF protoFunc  func
```

In this FUNCREF declaration, *protoFunc* is a function that specifies the format of the function that can be passed by the FUNCREF, and *func* is a function reference used as an input parameter.

When you declare a function reference variable within a user function, the syntax is:


```igor
FUNCREF protoFunc func = funcSpec
```

Here, the local FUNCREF variable, *func*, is assigned a *funcSpec*, which can be a literal function name, a $ string expression that evaluates at runtime, or another FUNCREF variable.

### *See Also* {#funcref-see-also}
[Function References](/igorpro/programming/programming.md#function-references)

<div className="command-signature">

## <strong>NVAR</strong> {#nvar}

</div>

NVAR is a declaration that creates a local reference to a global numeric variable accessed in a user-defined function.

The syntax of the NVAR declaration is:


```igor
NVAR [/C][/Z][/SDFR=dfr] localName [= pathToVar ][, localName1 [= pathToVar1 ]]...
```

The NVAR declaration is required when you access a global numeric variable in a function. At compile time, the NVAR statement tells Igor that the local name references a global numeric variable. At runtime, Igor makes the connection between the local name and the actual global variable. For this connection to be made, the global numeric variable must exist when the NVAR statement is executed.

When *localName* is the same as the global numeric variable name and you want to reference a global variable in the current data folder, you can omit *pathToVar*.

*pathToVar* can be a full literal path (e.g., root:FolderA:var0), a partial literal path (e.g., :FolderA:var0) or $ followed by string variable containing a computed path (see [Converting a String into a Reference Using $](/igorpro/programming/programming.md#converting-a-string-into-a-reference-using)).

You can also use a data folder reference or the /SDFR flag to specify the location of the numeric variable if it is not in the current data folder. See [Data Folder References](/igorpro/programming/programming.md#data-folder-references) and [The /SDFR Flag](/igorpro/programming/programming.md#the-sdfr-flag) for details.

If the global variable may not exist at runtime, use the /Z flag and call NVAR_Exists before accessing the variable. The /Z flag prevents Igor from flagging a missing global variable as an error and dropping into the Igor debugger. For example:


```igor
NVAR/Z nv=<pathToPossiblyMissingNumericVariable>
if( NVAR_Exists(nv) )
	<do something with nv>
endif
```

Note that to create a global numeric variable, you use the [Variable](/igorpro/commands/variable.md)/G operation.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Complex variable. |
| <span class="table-cell-nowrap">/SDFR = *dfr*</span> | Specifies the source data folder. See [The /SDFR Flag](/igorpro/programming/programming.md#the-sdfr-flag) for details. |
| <span class="table-cell-nowrap">/Z</span> | Ignore variable reference checking failures. |

### *See Also* {#nvar-see-also}
[NVAR_Exists](/igorpro/commands/nvar_exists.md)

[Accessing Global Variables And Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)

[Converting a String into a Reference Using $](/igorpro/programming/programming.md#converting-a-string-into-a-reference-using)

<div className="command-signature">

## <strong>STRUCT</strong> {#struct}

</div>
STRUCT is a declaration that creates a local reference to a Structure accessed in a user-defined function. When a Structure is passed to a user function, it can only be passed by reference, so in the declaration within the function you must use &localStructName to define the function input parameter.

The syntax of the STRUCT declaration is:

```igor
STRUCT structureName localName 
```

### *See Also* {#struct-see-also}
[Structures in Functions](/igorpro/programming/programming.md#structures-in-functions)

See the [Structure](/igorpro/programming/keywords/procedure-declaration-keywords.md#structure) keyword for creating a Structure definition.

<div className="command-signature">

## <strong>SVAR</strong> {#svar}

</div>

SVAR is a declaration that creates a local reference to a global string variable accessed in a user-defined function.

The syntax of the SVAR declaration is:


```igor
SVAR [/Z][/SDFR=dfr] localName [= pathToStr ][, localName1 [= pathToStr1 ]]...
```

The SVAR declaration is required when you access a global string variable in a function. At compile time, the SVAR statement tells Igor that the local name references a global string variable. At runtime, Igor makes the connection between the local name and the actual global variable. For this connection to be made, the global string variable must exist when the SVAR statement is executed.

When *localName* is the same as the global string variable name and you want to reference a global variable in the current data folder, you can omit *pathToStr*.

*pathToStr* can be a full literal path (e.g., root:FolderA:var0), a partial literal path (e.g., :FolderA:var0) or $ followed by string variable containing a computed path (see [Converting a String into a Reference Using $](/igorpro/programming/programming.md#converting-a-string-into-a-reference-using)).

You can also use a data folder reference or the /SDFR flag to specify the location of the string variable if it is not in the current data folder. See [Data Folder References](/igorpro/programming/programming.md#data-folder-references) and [The /SDFR Flag](/igorpro/programming/programming.md#the-sdfr-flag) for details.

If the global variable may not exist at runtime, use the /Z flag and call SVAR_Exists before accessing the variable. The /Z flag prevents Igor from flagging a missing global variable as an error and dropping into the Igor debugger. For example:


```igor
SVAR/Z nv=<pathToPossiblyMissingStringVariable>
if( SVAR_Exists(sv) )
	<do something with sv>
endif
```

Note that to create a global string variable, you use the [String](/igorpro/commands/string.md)/G operation.

### *Flags* {#svar-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/SDFR = *dfr*</span> | Specifies the source data folder. See [The /SDFR Flag](/igorpro/programming/programming.md#the-sdfr-flag) for details. |
| <span class="table-cell-nowrap">/Z</span> | An SVAR reference to a null string variable does not cause an error or debugger break. |

### *See Also* {#svar-see-also}
[SVAR_Exists](/igorpro/commands/svar_exists.md)

[Accessing Global Variables And Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)

[Converting a String into a Reference Using $](/igorpro/programming/programming.md#converting-a-string-into-a-reference-using)

<div className="command-signature">

## <strong>WAVE</strong> {#wave}

</div>

WAVE is a declaration that tells Igor the nature of a user-defined function parameter or creates a local reference to a wave accessed in the body of a user-defined function.

The syntax of the WAVE reference is:


```igor
WAVE [/C][/T][/WAVE][/DF][/Z][/ZZ][/SDFR=dfr] localName [= pathToWave ][, localName1 [= pathToWave1 ]]...
```

The optional /SDFR flag and *pathToWave* parameter are used only in the body of a function, not in a parameter declaration.

The WAVE declaration is required when you use a wave in an assignment statement in a function. At compile time, the WAVE statement tells Igor that the local name references a wave. At runtime, Igor makes the connection between the local name and the actual wave. For this connection to be made, the wave must exist when the WAVE statement is executed.

The WAVE declaration is also required if you use a wave name as a parameter to an operation or function if [rtGlobals](/igorpro/programming/keywords/other-programming-keywords.md#rtglobals)=3 is in effect which is the usual case.

When *localName* is the same as the global wave name and you want to reference a wave in the current data folder, you can omit the *pathToWave*.

*pathToWave* can be a full literal path (e.g., root:FolderA:wave0), a partial literal path (e.g., :FolderA:wave0) or $ followed by string variable containing a computed path (see [Converting a String into a Reference Using $](/igorpro/programming/programming.md#converting-a-string-into-a-reference-using)).

You can also use a data folder reference or the /SDFR flag to specify the location of the wave if it is not in the current data folder. See [Data Folder References](/igorpro/programming/programming.md#data-folder-references) and [The /SDFR Flag](/igorpro/programming/programming.md#the-sdfr-flag) for details.

If the wave may not exist at runtime, use the /Z flag and call [WaveExists](/igorpro/commands/waveexists.md) before accessing the wave. The /Z flag prevents Igor from flagging a missing wave as an error and dropping into the Igor debugger. For example:


```igor
WAVE/Z wv=<pathToPossiblyMissingWave>
if( WaveExists(wv) )
	<do something with wv>
endif
```

In Igor Pro 9.00 and later, you can avoid the runtime lookup of *localName* in the current data folder by including the /ZZ flag. For example:


```igor
Function CallingRoutine()
	WAVE/ZZ w
	PassByRefRoutine(w)
	Print w
End
Function PassByRefRoutine(WAVE& wr)
	WAVE wr = NewFreeWave(2,2)
End
```

Without the /ZZ flag, at runtime Igor would attempt to find a wave named w in the current data folder. This is unnecessary in this case since PassByRefRoutine sets the w variable.

### *Flags* {#wave-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Complex wave |
| <span class="table-cell-nowrap">/T</span> | Text wave |
| <span class="table-cell-nowrap">/WAVE</span> | Wave reference wave |
| <span class="table-cell-nowrap">/DF</span> | Data folder reference wave |
| <span class="table-cell-nowrap">/SDFR = *dfr*</span> | Specifies the source data folder. See [The /SDFR Flag](/igorpro/programming/programming.md#the-sdfr-flag) for details. |
| <span class="table-cell-nowrap">/Z</span> | Ignores wave reference checking failures |
| <span class="table-cell-nowrap">/ZZ</span> | Ignores wave reference checking failures and prevents wave lookup |

### *See Also* {#wave-see-also}
[WaveExists](/igorpro/commands/waveexists.md)

[WAVE Reference Type Flags](/igorpro/programming/programming.md#wave-reference-type-flags) for additional wave type flags and information.

[Accessing Global Variables And Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)

[Accessing Waves In Functions](/igorpro/programming/programming.md#accessing-waves-in-functions)

[Converting a String into a Reference Using $](/igorpro/programming/programming.md#converting-a-string-into-a-reference-using)

<div className="command-signature">

## <strong>WAVEClear</strong>  <em>localName</em>  [, <em>localName1</em>...] {#waveclear}

</div>

The WAVEClear operation clears out a wave reference variable. WAVEClear is equivalent to WAVE/Z localName= $"".

### *Details* {#details}
Use WAVEClear to avoid unexpected results from certain operations such as [Duplicate](/igorpro/commands/duplicate.md) or [Concatenate](/igorpro/commands/concatenate.md), which will reuse the contents of a WAVE reference variable and may not generate the wave in the desired data folder or with the desired name.

WAVEClear ensures that memory is deallocated after waves are killed as in this example:


```igor
Function foo()
	Make wave1
	FunctionThatKillsWave1()
	WAVEClear wave1
	AnotherFunction()
End
```

Although memory used for wave1 will be deallocated when foo returns, that memory will not be automatically released while the function executes because the WAVE variable still contains a reference to the wave. In this example, WAVEClear deallocates that memory before AnotherFunction executes.

You can also use WAVEClear before passing a data folder to preemptive threads using [ThreadGroupPutDF](/igorpro/commands/threadgroupputdf.md).

### *See Also* {#waveclear-see-also}
[Accessing Waves In Functions](/igorpro/programming/programming.md#accessing-waves-in-functions)

[Wave Reference Counting](/igorpro/programming/programming-techniques.md#wave-reference-counting)

[ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)