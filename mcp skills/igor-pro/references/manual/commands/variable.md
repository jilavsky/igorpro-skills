---
description: "The Variable operation creates real or complex variables and gives them the specified name."
slug: /commands/variable
---

<div className="command-signature">

## <strong>Variable</strong>  [/C/D/G] <em>varName</em>[/N=<em>name</em>][=<em>numExpr</em> ][, <em>varName</em>[/N=<em>name</em>][=<em>numExpr</em> ]]... {#variable}

</div>

The Variable operation creates real or complex variables and gives them the specified name.

### *Flags* {#flags}
|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | Declares a complex variable. |
| <span class="table-cell-nowrap">/D</span> | Obsolete, included only for backward compatibility (see Details). |
| <span class="table-cell-nowrap">/G</span> | Creates a variable with global scope and overwrites any existing variable. |
| <span class="table-cell-nowrap">/N = *name*</span> | Specifies a local name for the global numeric variable. /N was added in Igor Pro 8.00 and is available in user-defined functions only. See ***NVAR Creation*** below for details. |

### *Details* {#details}

The variable is initialized when it is created if you supply the initial value. However, when Variable is used to declare a function parameter, it is an error to attempt to initialize it.

You can create more than one variable at a time by separating the names and optional initializers for multiple variables with a comma.

Numeric variables are double precision. In ancient times, variables could be single or double precision and the /D flag meant double precision. The /D flag is allowed for backward compatibility but is no longer needed and should not be used in new code.

If used in a macro or function the new variable is local to that macro or function unless the /G flag is used. If used on the command line, the new variable is global.

*varName* can include a data folder path.

### *NVAR Creation* {#nvar-creation}

In a user-defined function, you need a local NVAR reference to access a global string variable. If you use a simple name rather than a path, Igor automatically creates an NVAR:

```igor
Variable/G nVar1                // Creates an NVAR named nVar1
```

If you use a path or a $ expression, Igor does not create an automatic NVAR reference. You can explicitly create NVARs like this:

```igor
Variable/G root:nVar2
NVAR nVar2 = root:nVar2         // Creates an NVAR named nVar2
String path = "root:nVar3"
Variable/G $path
NVAR nVar3 = $path              // Creates an NVAR named nVar3
```

In Igor Pro 8.00 and later, you can explicitly create an NVAR reference in a user-defined function using the /N flag, like this:

```igor
Variable/G nVar4/N=nVar4        // Creates an NVAR named nVar4
Variable/G root:nVar5/N=nVar5   // Creates an NVAR named nVar5
String path = "root:nVar6"
Variable/G $path/N=nVar6        // Creates an NVAR named nVar6
```

The name used for the NVAR does not need to be the same as the name of the global variable:

```igor
Variable/G nVar7/N=nv7	// Creates an NVAR named nv7
Variable/G root:nVar8/N=nv8	// Creates an NVAR named nv8
String path = "root:nVar9"
Variable/G $path/N=nv9	// Creates an NVAR named nv9
```

### *Examples* {#examples}

To initialize a complex variable, use the cmplx() function. For example:

```igor
Variable /C cv1 = cmplx(1,2)
```

This sets the real part of cv1 to 1 and the imaginary part to 2.

### *See Also* {#see-also}
[Numeric Variables](/igorpro/igor-basics/variables.md#numeric-variables), [Accessing Global Variables and Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves)