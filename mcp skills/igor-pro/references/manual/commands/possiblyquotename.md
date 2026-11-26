---
description: "The PossiblyQuoteName string function returns the input name string if it conforms to the rules of standard wave or Data Folder names."
slug: /commands/possiblyquotename
---

<div className="command-signature">

## <strong>PossiblyQuoteName</strong> (<em>nameStr</em>) {#possiblyquotename}

</div>

The PossiblyQuoteName string function returns the input name string if it conforms to the rules of standard wave or Data Folder names. If it does not, then the name is returned in single quotes. This is used when generating a command string that you will pass to the Execute command. You might get the input name string from a function such as NameOfWave() or CsrXWave().

### *Examples* {#examples}

```igor
Print PossiblyQuoteName("wave0")    // prints wave0
Print PossiblyQuoteName("wave 0")   // prints 'wave 0'
```

### *Details* {#details}
See [Programming with Liberal Names](/igorpro/programming/programming-techniques.md#programming-with-liberal-names).