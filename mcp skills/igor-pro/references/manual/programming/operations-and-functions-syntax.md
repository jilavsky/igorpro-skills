---
description: "External operations (XOPs) and external functions (XFUNCs) are not covered here."
slug: /programming/operations-and-functions-syntax
---

External operations (XOPs) and external functions (XFUNCs) are not covered here. For information about them, use the Command Help tab of the Igor Help Browser and the XOP help file in the same folder as the XOP file.

In the descriptions of functions and operations that follow, italics indicate parameters for which you can supply numeric or string expressions. Non-italic keywords must be entered literally as they appear. Commas, slashes, braces and parentheses in these descriptions are always literals. Brackets surround optional flags or parameters. Ellipses (...) indicate that the preceding element may be repeated a number of times.

Italicized parameters represent values you supply. Italic words ending with "Name" are names (wave names, for example), and those ending with "Str" are strings. Italic words ending with "Spec" (meaning "specification") are usually further defined in the description. If none of these endings are employed, the italic word is a numeric expression, such as a literal number, the name of a variable or function, or some valid combination.

Strings and names are different, but you can use a string where a name is expected using "string substitution": precede a string expression with the $ operator. See [String Substitution Using $](/igorpro/programming/commands.md#string-substitution-using).

The syntax description may span several lines, but the actual command you create must occupy a single line.

Many operations have optional "flags". Flags that accept a value (such as the Make operation's /N=*n*  flag; here *n*  is the value) sometimes require additional parentheses. For example:

```igor
Make/N=1 aNewWave
```

is acceptable because here *n* is the literal "1". To use a numeric expression (anything other than a literal number) for *n*, parentheses are needed:

```igor
Make/N=(numberOfPoints) aNewWave	// error if no parentheses!
```

For more about using functions, operations, and keywords, see [Working with Commands](/igorpro/programming/commands.md), [Programming Overview](/igorpro/programming/programming.md), and [Operations in Functions](/igorpro/programming/programming.md#operations-in-functions).