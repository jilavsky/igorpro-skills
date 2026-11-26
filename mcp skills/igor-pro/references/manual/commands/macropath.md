---
description: "The MacroPath function returns a path to the file containing the named macro."
slug: /commands/macropath
---

<div className="command-signature">

## <strong>MacroPath</strong> (<em>macroNameStr</em>) {#macropath}

</div>

The MacroPath function returns a path to the file containing the named macro.

MacroPath was added in Igor Pro 9.01.

In this section, "macro" includes all types of interpreted procedures, namely procedures introduced by the [Macro](/igorpro/programming/keywords/procedure-declaration-keywords.md#macro), [Proc](/igorpro/programming/keywords/procedure-declaration-keywords.md#proc) and [Window](/igorpro/programming/keywords/procedure-declaration-keywords.md#window) keywords.

### *Parameters* {#parameters}
If *macroNameStr* is "", MacroPath returns the path to the currently executing macro or "" if no macro is executing.

Otherwise MacroPath returns the path to the named macro or "" if no macro by that name exists.

### *Details* {#details}
MacroPath is useful in certain specialized cases, such as if a macro needs access to a lookup table of a large number of values.

The most likely use for this is to find the path to the file containing the currently running macro. This is done by passing "" for *macroNameStr*.

The returned path uses Macintosh syntax regardless of the current platform. See [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details.

If the procedure file is a normal standalone procedure file, the returned path will be a full path to the file.

If the macro resides in the built-in procedure window the returned path will be ":Procedure". If the macro resides in a packed procedure file, the returned path will be ":\<packed procedure window title\>".

If MacroPath is called when procedures are in an uncompiled state, it returns ":".

### *See Also* {#see-also}
[Macro](/igorpro/programming/keywords/procedure-declaration-keywords.md#macro), [Proc](/igorpro/programming/keywords/procedure-declaration-keywords.md#proc), [Window](/igorpro/programming/keywords/procedure-declaration-keywords.md#window), [MacroList](/igorpro/commands/macrolist.md), [MacroInfo](/igorpro/commands/macroinfo.md), [FunctionPath](/igorpro/commands/functionpath.md)