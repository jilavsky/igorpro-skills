---
description: "Use the following keywords to declare procedures of various kinds. These keywords always appear in an Igor procedure window, not in the command line."
slug: /programming/keywords/procedure-declaration-keywords
---

Use the following keywords to declare procedures of various kinds. These keywords always appear in an Igor procedure window, not in the command line.

<div className="command-signature">

## <strong>End</strong> {#end}

</div>

The End keyword signals the end of a macro, function, or menu definition. See [Function](/igorpro/programming/keywords/procedure-declaration-keywords.md#function) for an example.

<div className="command-signature">

## <strong>EndMacro</strong> {#endmacro}

</div>

The EndMacro keyword signals the end of a macro. You can also use the End keyword to end a macro. See [Macro](/igorpro/programming/keywords/procedure-declaration-keywords.md#macro) for an example.

<div className="command-signature">

## <strong>EndStructure</strong> {#endstructure}

</div>

The EndStructure keyword marks the end of a [Structure](/igorpro/programming/keywords/procedure-declaration-keywords.md#structure) definition.

<div className="command-signature">

## <strong>Function</strong>  [ /C /D /S /DF /WAVE ] {#function}

</div>

The Function keyword introduces a user-defined function in a procedure window.

The optional flags specify the return value type, if any, for the function.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Returns a complex number. |
| <span class="table-cell-nowrap">/D</span> | Returns a double-precision number. Obsolete, accepted for backward compatibility. |
| <span class="table-cell-nowrap">/S</span> | Returns a string. |
| <span class="table-cell-nowrap">/DF</span> | Returns a data folder reference. See [Data Folder Reference Function Results](/igorpro/programming/programming.md#data-folder-reference-function-results). |
| <span class="table-cell-nowrap">/WAVE</span> | Returns a wave reference. See [Wave Reference Function Results](/igorpro/programming/programming.md#wave-reference-function-results). |

### *Details* {#details}
If you omit all flags, the result is a scalar double-precision number.

The /D flag is not needed because all numeric return values are double-precision.

### *See Also* {#see-also}
[User-defined Functions](/igorpro/programming/programming.md#user-defined-functions), [Programming Overview](/igorpro/programming/programming.md)

<div className="command-signature">

## <strong>Macro</strong> {#macro}

</div>

The Macro keyword is used in a procedure window and introduces a procedure whose name you want to appear in the Macros menu. For example:


```igor
Macro TestMacro()
	Print "Hello, world!"
EndMacro
```

For most purposes, it is better to use Function instead of Macro, because functions run faster and have other advantages.

### *See Also* {#macro-see-also}
[Macros](/igorpro/programming/macros.md), [User-defined Functions](/igorpro/programming/programming.md#user-defined-functions), [Programming Overview](/igorpro/programming/programming.md)

<div className="command-signature">

## <strong>Picture</strong> {#picture}

</div>

The Picture keyword introduces an ASCII code picture definition of binary image data. For example:


```igor
// PNG: width= 56, height= 44
Picture myPictName
	ASCII85Begin
	M,6r;%14!\!!!!.8Ou6I!!!!Y!!!!M#Qau+!5G;q_uKc;&TgHDFAm*iFE_/6AH5;7DfQssEc39jTBQ
	=U!7FG,5u`*!m?g0PK.mR"U!k63rtBW)]$T)Q*!=Sa1TCDV*V+l:Lh^NW!fu1>;(.<VU1bs4L8&@Q_
	<4e(%"^F50:Jg6);j!CQdUA[dh6]%[OkHSC,ht+Q7ZO#.6U,IgfSZ!R1g':oO_iLF.GQ@RF[/*G98D
	bjE.g?NCte(pX-($m^\_FhhfL`D9uO6Qi5c[r4849Fc7+*)*O[tY(6<rkm^)/KLIc]VdDEbF-n5&Am
	2^hbTu:U#8ies_W<LGkp_LEU1bs4L8&?fqRJ[h#sVSSz8OZBBY!QNJ
	ASCII85End
End
```

### *See Also* {#picture-see-also}
[Proc Pictures](/igorpro/programming/programming.md#proc-pictures)

<div className="command-signature">

## <strong>Proc</strong> {#proc}

</div>

The Proc keyword is used in a procedure window and introduces a procedure whose name you do not want to appear in the Macros menu. For example:


```igor
Proc TestProc()
	Print "Hello, world!"
End
```

A Proc is a type of macro. For most purposes, it is better to use Function instead of Proc, because functions run faster and have other advantages.

### *See Also* {#proc-see-also}
[Macros](/igorpro/programming/macros.md), [User-defined Functions](/igorpro/programming/programming.md#user-defined-functions), [Programming Overview](/igorpro/programming/programming.md)

<div className="command-signature">

## <strong>Structure</strong> {#structure}

</div>

The Structure keyword introduces a structure definition in a user function. Within the body of the structure you declare the member type (*memType*) and the corresponding member name(s) (*memName*). Each *memName* may be declared with an optional array size.

Structure declarations have the format:


```igor
Structure structureName
	memType memName [arraySize ] [, memName [arraySize ]]
	...
EndStructure
```

### *Details* {#structure-details}
Structure member types (*memType*) can be any of the following Igor objects: Variable, String, WAVE, NVAR, SVAR, DFREF, FUNCREF, or STRUCT.

Igor structures also support additional member types, as given in the next table, for compatibility with C programming structures and disk files.

| Igor Member Type | C Equivalent | Size |
| --- | --- | --- |
| char | signed 8-bit int | 1 byte |
| uchar | unsigned 8-bit int | 1 byte |
| int16 | signed16-bit int | 2 bytes |
| uint16 | unsigned 16-bit int | 2 bytes |
| int32 | signed32-bit int | 4 bytes |
| uint32 | unsigned 32-bit int | 4 bytes |
| int64 | signed 64-bit int | 8 bytes (requires Igor Pro 7.00 or later) |
| uint64 | unsigned 64-bit int | 8 bytes (requires Igor Pro 7.00 or later) |
| float | float | 4 bytes |
| double | double | 8 bytes |

The Variable and double types are identical although Variable can be also specified as complex (using the /C flag).

Each structure member may have an optional arraySize specification, which gives the number of elements contained by the structure member. The array size is an integer number from 1 to 400 except for members of type STRUCT for which the upper limit is 100.

### *See Also* {#structure-see-also}
[Structures in Functions](/igorpro/programming/programming.md#structures-in-functions) for further information.

See the [STRUCT](/igorpro/programming/keywords/object-reference-keywords.md#struct) declaration for creating a local reference to a Structure.

<div className="command-signature">

## <strong>Window</strong> {#window}

</div>

The Window keyword is used in a procedure window and introduces a window recreation procedure. For example:


```igor
Window Graph0() : Graph
	Display wave0
	ModifyGraph rgb(wave0)=(0,0,65535)
End
```

A Window recreation procedure is a type of macro. Igor automatically creates a window recreation macro when you close a graph, table, layout, control panel, or XOP target window. The name of each window recreation macro appears in a submenu in the Windows menu, such as the Graph Macros submenu.

Except in rare circumstances, a programmer should not use the Window keyword, but should use [Macro](/igorpro/programming/keywords/procedure-declaration-keywords.md#macro), [Proc](/igorpro/programming/keywords/procedure-declaration-keywords.md#proc), or [Function](/igorpro/programming/keywords/procedure-declaration-keywords.md#function) instead. For most purposes, it is best to use Function because functions run faster and have other advantages.

### *See Also* {#window-see-also}
[Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro)