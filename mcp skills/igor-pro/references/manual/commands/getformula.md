---
description: "The GetFormula function returns a string containing the named object's dependency formula. The named object must be a wave, numeric variable or string variable."
slug: /commands/getformula
---

<div className="command-signature">

## <strong>GetFormula</strong> (<em>objName</em>) {#getformula}

</div>

The GetFormula function returns a string containing the named object's dependency formula. The named object must be a wave, numeric variable or string variable.

### *Details* {#details}
Normally an object will have an empty dependency formula and GetFormula will return an empty string (""). If you assign a expression to an object using the := operator or the SetFormula operation, the text on the right side of the := or the parameter to SetFormula is the object's dependency formula and this is what GetFormula will return.

### *Examples* {#examples}

```igor
Variable/G dependsOnIt
Make/O wave0 := dependsOnIt*2	// wave0 changes when dependsOnItdoes
Print GetFormula(wave0)
```

Prints the following in the history area:


```
dependsOnIt*2
```

### *See Also* {#see-also}
[Dependencies](/igorpro/programming/dependencies.md), [SetFormula](/igorpro/commands/setformula.md)