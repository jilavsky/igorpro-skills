---
description: "The UniqueName function returns the concatenation of baseName and a number such that the result is not in conflict with any other object name."
slug: /commands/uniquename
---

<div className="command-signature">

## <strong>UniqueName</strong> (<em>baseName</em>, <em>objectType</em>, <em>startSuffix</em> [, <em>windowNameStr</em>]) {#uniquename}

</div>

The UniqueName function returns the concatenation of *baseName* and a number such that the result is not in conflict with any other object name.

*WindowNameStr* is optional. If missing, it is taken to be the top graph, panel, layout, or notebook according to the value of *objectType*.

In Igor Pro 9.00 or later, you can use the [CreateDataObjectName](/igorpro/commands/createdataobjectname.md) function as a replacement for some combination of CheckName, CleanupName, and UniqueName to create names of waves, global variables, and data folders.

### *Details* {#details}
*baseName* should be an unquoted name, such as you might receive from the user through a dialog or control panel.

*objectType* is one of the following:

|  |  |
| --- | --- |
| 1: | Wave |
| 2: | Reserved |
| 3: | Numeric variable |
| 4: | String variable |
| 5: | XOP target window |
| 6: | Graph window |
| 7: | Table window |
| 8: | Layout window |
| 9: | Control panel window |
| 10: | Notebook window |
| 11: | Data folder |
| 12: | Symbolic path |
| 13: | Picture |
| 14: | Annotation in the named or topmost graph or layout |
| 15: | Control in the named or topmost graph or panel |
| 16: | Notebook action character in the named or topmost notebook |
| 17: | Gizmo window (added in Igor Pro 9.00) |

*startSuffix* is the number used as a starting point when generating the numeric suffix that makes the name unique. Normally you should pass zero for *startSuffix* . If you know that names of the form base0 through baseN are in use, you can make UniqueName run a bit faster by passing N+1 as the *startSuffix*.

The *windowNameStr* argument is used only with object types 14, 15 and 16. The returned name is unique only to the window (other windows might have objects with the same name). If a named window is given but does not exist, UniqueName returns *baseName* *startSuffix. windowNameStr* is ignored for other object types.

### *The Main Namespace* {#the-main-namespace}
Waves, numeric variables, string variables, built-in and external functions, built-in and external operations, user-defined functions, macros and reserved keywords exist in the main namespace. The names of each of those objects must be unique in that namespace.

### *Window Namespace* {#window-namespace}
Values of *objectType* from 5 through 10 refer to the window namespace.

The expression


```igor
CheckName("<name>", x)	// where x is 5, 6, 7, 8, 9 or 10
```

returns 0 if the specified name is syntactically legal and unique in the window namespace.

That does not guarantee that the name is allowed as a window name because the DoWindow/C operation, which changes a window's name, requires that the name also not conflict with objects in the main namespace. Consequently, to determine if a name is allowed as a window name, use this:


```igor
// Window names must be unique in both the window and main namespaces
Variable nameOK = CheckName("<name>",6)==0 && CheckName("<name>",1)==0
```

### *Window Macro Names* {#window-macro-names}
Window macro names are treated different from other main namespace names. DoWindow/C allows you to change the name of a window to the name of an existing window macro but not to any other name in the main namespace. Also this expression:


```igor
CheckName("<name>", x)	// where x is 1, 3, 4 (main namespace)
```

returns 0 even if the specified name is used as a window macro name.

### *UniqueName Thread Safety* {#uniquename-thread-safety}
As of Igor Pro 8.00, you can call UniqueName from an Igor preemptive thread but only if *objectType* is 1 (wave), 3 (global numeric variable), 4 (global string variable), 11 (data folder) or 12 (symbolic path). For any other value of *objectType*, UniqueName returns a runtime error.

### *Examples* {#examples}

```igor
String uniqueWaveName = UniqueName(baseWaveName, 1, 0)
String uniqueControlName = UniqueName("ctrl", 15, 0, "Panel0")
```

### *See Also* {#see-also}
[Object Names](/igorpro/igor-basics/using-igor.md#object-names), [Programming With Liberal Names](/igorpro/programming/programming-techniques.md#programming-with-liberal-names), [CreateDataObjectName](/igorpro/commands/createdataobjectname.md), [CheckName](/igorpro/commands/checkname.md), [CleanupName](/igorpro/commands/cleanupname.md)