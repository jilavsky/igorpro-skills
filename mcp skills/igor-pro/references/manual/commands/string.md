---
description: "The String operation creates string variables and gives them the specified names."
slug: /commands/string
---

<div className="command-signature">

## <strong>String</strong>  [/G] <em>strName</em>[/N=<em>name</em>][=<em>strExpr</em> ] [, <em>strName</em>[/N=<em>name</em>][=<em>strExpr</em> ]... ] {#string}

</div>

The String operation creates string variables and gives them the specified names.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/G</span> | Creates a global string. Any existing string with the specified name is overwritten. |
| <span class="table-cell-nowrap">/N = name</span> | Specifies a local name for the global string variable. /N was added in Igor Pro 8.00 and is available in user-defined functions only. See ***SVAR Creation*** below for details. |

### *Details* {#details}

The string variable is initialized when it is created if you supply the =*strExpr* initializer. However, when String is used to declare a function parameter, it is an error to attempt to initialize it.

You can create more than one string variable at a time by separating the names and optional initializers with commas.
If used in a procedure, the new string is local to that procedure unless the /G flag is used. If used on the command line, 

`String` is equivalent to `String/G`.

*strName* can optionally include a data folder path.

### *SVAR Creation* {#svar-creation}

In a user-defined function, you need a local SVAR reference to access a global string variable. If you use a simple name rather than a path, Igor automatically creates an SVAR:

```igor
String/G sVar1                  // Creates an SVAR named sVar1
```

If you use a path or a $ expression, Igor does not create an automatic SVAR reference. You can explicitly create SVARs like this:

```igor
String/G root:sVar2
SVAR sVar2 = root:sVar2         // Creates an SVAR named sVar2
String path = "root:sVar3"
String/G $path
SVAR sVar3 = $path              // Creates an SVAR named sVar3
```

In Igor Pro 8.00 and later, you can explicitly create an SVAR reference in a user-defined function using the /N flag, like this:

```igor
String/G sVar4/N=sVar4          // Creates an SVAR named sVar4
String/G root:sVar5/N=sVar5     // Creates an SVAR named sVar5
String path = "root:sVar6"
String/G $path/N=sVar6          // Creates an SVAR named sVar6
```

The name used for the SVAR does not need to be the same as the name of the global variable:

```igor
String/G sVar7/N=sv7            // Creates an SVAR named sv7
String/G root:sVar8/N=sv8       // Creates an SVAR named sv8
String path = "root:sVar9"
String/G $path/N=sv9            // Creates an SVAR named sv9
```

### *See Also* {#see-also}
[String Variables](/igorpro/igor-basics/variables.md#string-variables), [Working With Strings](/igorpro/programming/commands.md#working-with-strings), [Accessing Global Variables and Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)